<template>
    <section>
        <div v-if="produto" class="produto">
            <ul class="fotos" v-if="produto.fotos">
                <li v-for="(fotos,index) in produto.fotos" :key="index">
                    <img :src="foto.src" :alt="foto.titulo" />
                </li>
            </ul>
            <div class="info">
                <h1 v-text="produto.nome"></h1>
                <p class="preco" 
                   v-text="produto.preco" ></p>
                <p class="descricao"
                   v-text="produto.descricao"></p>
                <button class="btn" v-if="produto.vendido ==='false'" >Comprar</button>  
                <button class="btn" v-else disabled>Produto Vendido</button>    
            </div>
        </div>
        <PaginaCarregando v-else />
    </section>
</template>

<script>
import PaginaCarregando from '../components/PaginaCarregando.vue';
import {api} from '../services/services';

export default {
    components: { PaginaCarregando },
  name: 'Produto',
  props:["id"],
  data(){
    return{
      produto : null
    }
  },
  methods:{
    getProduto(){
      api.get(`/produto/${this.id}`).then(response=>{this.produto = response.data})
    }
  },
  created(){
    this.getProduto()
  }
}
</script>
<style  scoped>
    .produto{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap:30px;
        max-width: 900px;
        padding: 60px 20px;
        margin: 0 auto;
    }
    .preco{
        color: #e80;
        font-weight: bold;
        font-size: 1.5rem;
        margin-bottom: 40px; 
    }

    .descricao{
         font-size: 1.2rem;
    }
    
    .btn{
        margin-top:60px;
    }

</style>