<template>
  <Banner/>
  <h1>Formulário para Montar o Hanburger</h1>
  <BurgerForm/>
</template>


<script>
import Banner from '../components/banner.vue'
import BurgerForm from '../components/BurgerForm.vue'
export default{
  name:"Home",
  components:{
      Banner,
      BurgerForm,

  }
}


</script>
