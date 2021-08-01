<template>
  <section class="produtos-container">
    <transition mode="out-in">
    <div v-if="produtos && produtos.length >0" class="produtos" key="produtos">
      <div class="produto" v-for="(item,index) in produtos" :key="index">  
        <router-link :to="{name:'Produto' ,params:{id:item.id}}">   
          <img v-if="item.fotos" src="item.fotos[0].src" alt="item.fotos[0].titulo" >
          <p class="preco">{{item.preco}}</p>
          <h2 class="titulo">{{item.nome}}</h2>
          <p>{{item.descricao}}</p>
        </router-link>
      </div>   
       <produtos-paginar 
      :produtosTotal="produtos_total"
      :produtosPorPagina="produtos_pagina"
      >
      </produtos-paginar>
    </div>
    <div  v-else-if="produtos && produtos.length ===0" key="sem-resultados">
        <p class="sem-resultado">Busca sem resultados, tente outro termo</p>
    </div>
        <pagina-carregando key="carrgando" v-else></pagina-carregando>
    </transition>
  </section>
</template>

<script>
import ProdutosPaginar from "./ProdutosPaginar.vue";
import {api} from "../services/services";
import PaginaCarregando from './PaginaCarregando.vue';

export default {
  name: 'produto-lista',
  components:{
    ProdutosPaginar,
    PaginaCarregando
  },
  data(){
    return{
      produtos:null,
      produtos_pagina:5,
      produtos_total:0
    }
  },
  computed:{
    url(){
      let query_string = ""; 
      for(let key in this.$route.query){
        query_string += `&${key}=${this.$route.query[key]}`
      }

      return "/produto/?_limit="+this.produtos_pagina+ " "+query_string
    }
  },
  methods:{
    getProdutos(){
     this.produtos = null;
     window.setTimeout(()=>{
       api.get(this.url).then(response => {
        this.produtos_total = Number(response.headers['x-total-count']);
        this.produtos = response.data;
      });
     },1500);  
    }
  },
  watch:{
    url(){
      this.getProdutos()
    }
  },
  created(){
    this.getProdutos();
  }
}
</script>
<style scoped>
  .produtos-container{
    max-width: 2300px;
    margin: 0px;
  }
  .produtos{
    display: grid;
    grid-template-columns: repeat(3,1fr);
    grid-gap: 30px;
    margin: 30px;
  }
  .produto{
    box-shadow: 0 4px 8px rgba(30, 60, 90, 0.1);
    padding: 10px;
    background: #fff;
    border-radius:4px;
    transition:all 0.2s;
  }
  .produto:hover{
    box-shadow: 0 4px 8px rgba(30, 60, 90, 0.2);
    transform: scale(1.1);
    position: relative;
    z-index: 1;
  }

  .produto img{
    border-radius:4px;
    margin-bottom: 20px;
  }
  .titulo{
    margin-bottom: 10px;
  }
  .preco{
    color: #e80;
    font-weight: bold;
  }
  .sem-resultado{
    text-align: center;
  }
</style>
