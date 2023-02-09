<template>
<div>
    <Message :msg="msg" v-show="msg"/>
    <div>
        <form id="BurgerForm" @submit="IncluirBurger">
            <div class="InputConteiner">
                <label for="Nome">Nome do Cliente:</label>
                <input type="text" id="Nome" name="Nome" v-model="Nome" placeholder="Digite seu nome">
            </div>

            <div class="InputConteiner">
                <label for="Pao">Escolha o Pao</label>
                    <select name="Pao" id="Pao" v-model="Pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo" >{{pao.tipo}}</option>
                    </select>
            </div>


            <div class="InputConteiner">
                <label for="Carne">Escolha a Carne</label>
                    <select name="Carne" id="Carne" v-model="Carne">
                        <option value="">Selecione o tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo" >{{carne.tipo}}</option>
                    </select>
            </div>


            <div  id="OpcionaisConteiner" Class="InputConteiner">
                <label id="OpcionaisTitle"  for="Opcionais">Selecione os opcionais</label>
                
                <div class="CheckboxConteiner" v-for="opcional in OpcionaisData" :key="opcional.id" >
                    <input type="checkbox" name="Opcionais" v-model="Opcionais" :value="opcional.tipo">
                    <span>{{opcional.tipo}}</span>
                </div>

            </div>


            <div  class="InputConteiner">
                <input type="submit" class="SubmitBtn" value="Criar meu Burger!">
                
            </div>

        </form>
    </div>
</div>


</template>

<script>
import Message from './Message.vue';

export default {
  
    name:"BugerForm",
    data(){
        return{
            paes: null,
            carnes:null,
            OpcionaisData:null,
            Nome:null,
            Pao:null,
            Carne:null,
            Opcionais:[],
            msg: null,
        }
    }, 
    methods:{
        async getIngredientes(){
            const req= await fetch("http://localhost:3000/ingredientes");
            const data= await req.json();
            this.paes=data.paes;
            this.carnes=data.carnes;
            this.OpcionaisData=data.opcionais;
            
        },
        async IncluirBurger(e){
            e.preventDefault();
            
            const data ={
                nome:this.Nome,
                pao: this.Pao,
                carne: this.Carne,
                opcionais: Array.from(this.Opcionais),
                Status:"Solicitado",
            }
            console.log(data);

            const datajson = JSON.stringify(data);

            console.log(datajson)
            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: {"content-type":"application/json"},
                body: datajson
            })
            const res = await req.json();
            console.log(res);
            
            this.msg=`Seu pedido foi realizado, o código é ${res.id}`
            setTimeout(()=>this.msg="", 3000)
            
            //limpar campos
            this.Nome="";
            this.Pao=""
            this.Carne="";
            this.Opcionais="";

        }
    },
    mounted(){
        this.getIngredientes()
    },
    components:{
        Message
    }

}

</script>


<style scoped>

#BurgerForm{
    max-width: 400px;
    margin: 0 auto;

}
.InputConteiner{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;

}
label{
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}

input, select {
    padding: 5px 10px;
    width: 300px;

}
#OpcionaisConteiner{
    flex-direction: row;
    flex-wrap: wrap;
}
.OpcionaisTitle{
    max-width: 100%;
}

.CheckboxConteiner{
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.CheckboxConteiner span,
.CheckboxConteiner input{
    width: auto;
}
.CheckboxConteiner span{
    margin-left: 6px;
    font-weight: bold;


}
.SubmitBtn{
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor:pointer;
    transition: .5s;
}
.SubmitBtn:hover{
    background-color: transparent;
    color: #222;
}






</style>

