<template>
  <div class="custom-select rounded-lg" @click="toggleDropdown">
    <div class="selected-option h-[44px] flex items-center gap-[8px]">
      <slot></slot>
      <span class="opacity-50">{{ selectedOption }}</span>
    </div>
    <transition name="fade">
      <div v-if="isOpen" class="dropdown">
        <div v-for="option in options" :key="option" @click="selectOption(option)">
          {{ option }}
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  props: {
    value: {
      type: Number,
      required: true
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  setup(props, { emit }) {
    const isOpen = ref(false);
    const selectedOption = ref(props.value);

    const toggleDropdown = () => {
      isOpen.value = !isOpen.value;
    };

    const selectOption = (option) => {
      selectedOption.value = option;
      isOpen.value = false;
      emit('update:modelValue', option);
    };

    return {
      isOpen,
      selectedOption,
      toggleDropdown,
      selectOption
    };
  }
};
</script>

<style scoped>
.custom-select {
  @apply relative cursor-pointer;
}

.selected-option {
  @apply p-2 border border-gray-300 rounded-lg ;
}

.dropdown {
  @apply absolute top-full left-0 w-full max-h-48 overflow-y-auto bg-white border border-gray-300 border-t-0 rounded-b-md shadow-md;
}

.dropdown div {
  @apply p-2;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.2s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
