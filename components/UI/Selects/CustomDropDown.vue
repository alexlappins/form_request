<template>
    <div class="relative" >
      <div class="flex items-center gap-[8px]  select-header border border-gray-300 rounded-[8px] p-2 cursor-pointer" @click="toggleSelect">
        <slot></slot><span class="opacity-50">{{ selectedOptions.length ? selectedOptions.join(', ') : placeholder }}</span>
      </div>
      <transition name="slide-fade"  >
        <div v-if="isOpen" class="options-list absolute top-full left-0 w-full max-h-40 overflow-y-auto bg-white border border-gray-300 border-t-0 rounded-b-md shadow-md z-10">
          <div v-for="option in options" :key="option.id">
            <label class="block p-2" :for="option.id">
              <!-- <input type="checkbox" :id="option.id" v-model="selectedIds" :value="option.id" class="mr-2"> -->
              {{ option.label }}
            </label>
            <div v-if="option.children" class="children pl-8">
              <div v-for="child in option.children" :key="child.id">
                <label class="block p-2" :for="`${child.id + child.label}`" >
                  <input type="checkbox" :id="child.id" v-model="selectedIds" :value="child.id" class="mr-2">
                  {{ child.label }}
                </label>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        isOpen: false,
        selectedIds: []
      };
    },
    props: {
      options: {
        type: Array,
        default: () => []
      },
      placeholder: {
        type: String,
        default: 'Select'
      },
      
    },
    computed: {
      selectedOptions() {
        return this.options.flatMap(option => {
          if (this.selectedIds.includes(option.id)) {
            return option.label;
          } else if (option.children) {
            return option.children.flatMap(child => {
              return this.selectedIds.includes(child.id) ? child.label : [];
            });
          } else {
            return [];
          }
        });
      }
    },
    watch:{
        selectedIds(val){
            this.$emit('selectedOptions',val)
        }
    },
    methods: {
      toggleSelect() {
        this.isOpen = !this.isOpen;
      }
    }
  };
  </script>
  
  <style scoped>
  .slide-fade-enter-active,
  .slide-fade-leave-active {
    transition: opacity 0.2s, transform 0.2s;
  }
  
  .slide-fade-enter,
  .slide-fade-leave-to {
    opacity: 0;
    transform: translateY(-10px);
  }
  </style>
  