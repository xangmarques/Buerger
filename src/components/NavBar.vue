<template>
  <nav id="nav">
    <RouterLink to="/" id="LogoUrl">
        <img v-bind:src="Logo" v-bind:alt="Alt" id="Logo">
    </RouterLink>
    <router-link to="/">Home</router-link> |
    <router-link to="/Pedidos">Pedidos</router-link>
  </nav>
</template>

<script>
export default{
    name:"NavBar",
    props:["Logo","Alt"]

}
</script>

<style scoped>

  #nav{
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }
  #nav #LogoUrl{
    margin: auto;
    margin-left: 0;
  }
  #Logo{
    width: 40px;
    height: 40px;

  }
  #nav a{
    color: #fcba03;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
  }
  #nav a:hover {
    color: #fff ;
  }




</style>