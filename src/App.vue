
import NavBar from './components/NavBar.vue';

<template>
  <NavBar :Logo="Logo_Src" :alt="App_Name"/>
  <router-view/>
  <Footer/>
</template>

<script>

import NavBar from './components/NavBar.vue';
import Footer from './components/Footer.vue';

export default{
  components:{
    NavBar,
    Footer,
  },
  data(){
      return{
        Logo_Src: "/img/logo.png",
        App_Name: "Loja de Hamburger"
      }
  }
}

</script>



<style>
* {
  font-family: helvetica;
  padding: 0;
  margin: 0;
  box-sizing: border-box;
 
}
.MainContainer{
margin: 50px;
min-height: 300px;

}
h1{
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}


</style>
