<template>
    <div class="MessageContainer">
        <p>{{msg}}</p>

    </div>
</template>

<script>
    
export default {
    name:"Message",
    props:{
     msg: String
    }
  
}
</script>

<style scoped>
.MessageContainer{
    color: #005085;
    background-color: #cce5ff;
    border: 2px solid #88daff;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;

}



</style>