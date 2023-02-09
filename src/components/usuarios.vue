<template>
    <h1>Usuarios importados</h1>
</template>

<script>

import axios from "axios"


    name:"usuarios"
export default {
    data(){
        return{
            conteudo:null,
            data:[],
            columnNames:[
            "Login",
            "Nome",
            "Ramal",
            "StatusSistema",
            "StatusSistemaDesc",
            "StatusRamal",
            "StatusRamalDesc",
            "NomeDac"
            ]
        }
    },
    methods:{
        async getTotalIp(){
           axios
           .get("http://127.0.0.1:8080/api/usuarios?chave=747c65a44550c91cc00a9891dc36aa06")
           .then(response=>(this.conteudo=response))
            }
            
        },
    
    mounted(){
      this.getTotalIp();  
        
    }
}
    

</script>