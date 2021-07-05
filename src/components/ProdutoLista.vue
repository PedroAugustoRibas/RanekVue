<template>
  <section>
    <div v-for="(item,index) in produtos" :key="index">
       
        <img v-if="item.fotos" src="item.fotos[0].src" alt="item.fotos[0].titulo" >
        <p class="preco">{{item.preco}}</p>
        <h2 class="titulo">{{item.nome}}</h2>
        <p>{{item.descricao}}</p>

    </div>
    
  </section>
</template>

<script>
import {api} from "../services/services";

export default {
  name: 'produto-lista',
  data(){
    return{
      produtos:null
    }
  },
  methods:{
    getProdutos(){
     api.get("/produto").then(response => {
        this.produtos = response.data;
      });
    }
  },
  created(){
    this.getProdutos();
  }
}
</script>
