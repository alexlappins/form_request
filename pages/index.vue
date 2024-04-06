<template>
    <div>
      <FormRequest @requesForm="requesForm"></FormRequest>
      <div v-if="view">
        форма:{{ form_respons }}
        отправка формы произошла в файле index.vue ,в функции requestForm
      </div>
    </div>
</template>

<script setup>
import FormRequest from '../components/FormRequest.vue'
const form_respons = ref({})
const view = ref(false)
const setForm = (value)=>{
    form_respons.value = value
    view.value = !view.value
}
const requesForm = async (form)=>{
   await setForm(form)   // тут await поставлен что бы не было ошибок в коде ,так как await нужее в закомиченом коде 
    // тут бы я делал отправку формы на бек 
    // try{
    //  const respons = await axios.get('endpoint',{
    //     params:form
    //  })
    //  const form_respons = respons.data.data
    // }catch(error){
    //  console.log(error)
    // }
    // либо fetch 
   // try {
   // const response = await $fetch('endpoint', {
    //    method: 'GET',
    //    headers: {
   //         'Content-Type': 'application/json'
   //     },
   //     body: JSON.stringify(form)
  //  });
    
 //   if (!response.ok) {
   //     throw new Error('Network response was not ok');
  //  }

  //  const responseData = await response.json();
 //   const form_response = responseData.data;
//} catch (error) {
//    console.log(error);
//}
}
</script>
