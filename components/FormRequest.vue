<template>
    <div class="max-w-[1290px]  h-[133px] rounded-[16px] p-[20px] gap-[10px] bg-white bg-opacity-100">
        <div class="flex gap-[20px] w-full flex-wrap">
            <cusomDropDown @selectedOptions="selectedOptionsFrom" class="w-[190px] h-[44px]" :placeholder="'Откуда'" :options="countries"><img
                    src="../assets/svg/location.svg" /></cusomDropDown>
            <cusomDropDown @selectedOptions="selectedOptionsTo" :placeholder="'Куда'" class="w-[190px] h-[44px]" :options="countries"><img
                    src="../assets/svg/world.svg" /></cusomDropDown>
            <VueDatePicker :placeholder="'Период отбытия'" :range="{ partialRange: false }" class="!w-[190px] !h-[44px]"
                v-model="form.date">
            </VueDatePicker>
            <cusomSelect class="w-[190px] h-[44px]" v-model="form.count_days" :value="form.count_days"
                :options="option_counst"><img src="../assets/svg/Night.svg" /></cusomSelect>
            <cusomSelect class="w-[190px] h-[44px]" v-model="form.count_users" :value="form.count_users"
                :options="option_counst"><img src="../assets/svg/users.svg" /></cusomSelect>
            <custom-button class="w-[190px] h-[44px]" @click="handleButtonClick"> <img
                    src="../assets/svg/search.svg" /><span class="font-normal text-[16px]">Найти туры</span></custom-button>

        </div>
    </div>
</template>
<script setup>
import customButton from './UI/buttons/CustomButton.vue';
import cusomDropDown from './UI/Selects/CustomDropDown.vue'
import cusomSelect from './UI/Selects/CustomSelect.vue'
import VueDatePicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css'
import countriesjson from '../static/countries.json'
const form = ref({
    from_country: [],
    to_country:[],
    date: '',
    count_users: 0,
    count_days: 0,
})
const emit = defineEmits(['requesForm'])

const option_counst = [1, 2, 3, 4, 5]
const countries = ref([])
const handleButtonClick = () => {
    emit("requesForm",form.value)
}
const selectedOptionsFrom = (value)=>{
    form.value.from_country = value
}
const selectedOptionsTo = (value)=>{
    form.value.to_country = value
}
onMounted(() => {
    countries.value = countriesjson
})

</script>
<style>
.dp__input_wrap {
    height: 44px;
}

.dp__pointer {
    height: 44px;
    border-radius: 8px;

}
</style>