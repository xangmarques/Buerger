<template>
    
    <div id="BurgerTabela">
        <usuarios/>
        <Message :msg="msg" v-show="msg"/>
        <div>
            <div id="BurgerTabelaHeading">
                <div class="OrderId">#:</div>
                <div>Cliente</div>
                <div>Pão</div>
                <div>Carne</div>
                <div>Opcionais</div>
                <div>Ações</div>
                </div>
        </div>
        <div id="BurgerTabelaRows">
            <div class="BurgerTabelaRow" v-for="Burger in Burgers" :key="Burger.id">
                    
                    <div class="OrderNumero">{{Burger.id}}</div>
                    <div>{{Burger.nome}}</div>
                    <div>{{Burger.pao}}</div>
                    <div>{{ Burger.carne}}</div>
                    <div>
                        <ul>
                            <li v-for="(opcional,index) in Burger.opcionais" :key="index">{{opcional}}</li>
                            
                        </ul>
                    </div>
                    <div>
                            <select name="Status" class="Status" @change="AtualisarStatus($event,Burger.id)">
                                <option value="">Selecione</option>
                                <option v-for="s in Status" :key="s.id" :value="s.tipo" :selected="s.tipo==Burger.Status">{{s.tipo}}</option>
                            </select>
                        <button class="DeleteBtn" @click="DeletarBurger(Burger.id)">Cancelar</button>
                    </div>
                    
            </div>
        </div>
    </div>
</template>


<script>
import Message from './Message.vue';
import Usuarios from './usuarios.vue';

export default {
    name:"DashBoard",
    data(){
        return{
            Burgers: null,
            BurgerId: null,
            Status:[],
            msg:null
        }
    
    },
    components:{
      Message,  
      Usuarios
    },
   
        methods:{
        async GetPedidos(){
            const req = await fetch('http://localhost:3000/burgers')
            const data =  await req.json();
            this.Burgers=data;
            //resgatar os status depois 
            
            this.GetStatus()

            
        },
        async GetStatus(){
            const req = await fetch('http://localhost:3000/status')
            const data = await req.json();
            this.Status=data
            
        },


        async DeletarBurger(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                method: "Delete"
            })
            const res =await req.json();
            
            this.msg=`O pedido nº ${id} foi removido!`
            setTimeout(()=>this.msg="", 3000)
            this.GetPedidos()
        },


        async AtualisarStatus(evento,id){
            const option= evento.target.value;
            const datajson = JSON.stringify({Status:option})
            const req = await fetch(`http://localhost:3000/burgers/${id}`,
            {
                method:"PATCH",
                headers: {"Content-type": "application/json"},
                body:datajson
            });
            const res = await req.json();
            console.log(res)
            this.msg=`O pedido nº ${res.id} foi atualizado para "${res.Status}"`
            setTimeout(()=>this.msg="", 3000)

        }

    },
    mounted() {
        this.GetPedidos();

    },

        
 }

</script>

<style scoped>

#BurgerTabela{
    max-width: 1200px;
    margin: 0 auto;

}
#BurgerTabelaHeading,
#BurgerTabelaRows,
.BurgerTabelaRow{
    
    display: flex;
    flex-wrap: wrap;
}

#BurgerTabelaHeading{
 font-weight: bold;
 padding: 12px;
 border-bottom: 3px solid #333;

}
#BurgerTabelaHeading div,
.BurgerTabelaRow div {
    width: 19%

}

.BurgerTabelaRow{
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc
}
#BurgerTabelaHeading .OrderId,
.BurgerTabelaRow .OrderNumero{
    width: 5%;
}
Select {
    padding: 12px 6px;
    margin-right: 12px;
}
.DeleteBtn{
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border:2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: 0.5s;
}

.DeleteBtn:hover{
    background-color: transparent;
    color: #222;
}


</style>