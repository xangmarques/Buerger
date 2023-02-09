<template>
    <div id="MainBanner">
      <h1>Monte seu Hanburger</h1>
            
    </div>
</template>

<script>

export default{
    name:"Banner"

}

</script>

<style scoped>

#MainBanner{
  background-image: url("/inetpub/wwwroot/sig/public/img/burger.jpg");/*/inetpub/wwwroot/sig/public/*/
  background-position: 0 -500px;
  background-size:auto;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content:flex-start ;


}
#MainBanner h1 {
  color: white;
  text-align: center;
  font-size: 60px;
  background-color: #222;
  padding: 20px 40px;

}


</style>