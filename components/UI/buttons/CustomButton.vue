<template>
    <button @click="handleButtonClick" class=" flex items-center justify-center gap-[8px] bg-gradient-to-r from-purple-700 to-blue-500 text-white font-bold py-2 px-4 rounded">
        <slot></slot>
    </button>
</template>
<script>
export default{
    methods:{
        handleButtonClick(){
        this.$emit('handleButtonClick')
        },
    }
}
</script>
