<template>
 <form>
   <input name="busca" id="busca" placeholder="Buscar..." type="text" v-model="busca" />
   <input type="submit" id="lupa" value="buscar" @click.prevent="buscarProdutos" />
 </form>
</template>

<script>
export default {
  name: 'produto-buscar',
  methods:{
    buscarProdutos(){
      this.$router.push({query:{q:this.busca}})
    }
  },
  data(){
    return{
      busca:null
    }
  }
}
</script>


<style scoped>
form{
  max-width: 600px;
  margin: 30px auto 60px auto;
  position: relative;
}

#busca {
  width: 100%;
  padding: 20px;
  border: none;

}
#busca:focus,
#busca:hover{
  outline: none;
  transform: scale(1.1);
  box-shadow: 0 4px 8px rgba(30, 60, 90, 0.2);
}

#lupa{
  width: 62px;
  height: 62px;
  background: url('../assets/search.svg')no-repeat center center;
  text-indent: -150px;
  border: none;
  cursor: pointer;
  position: absolute;
  top:0px;
  right: 0px;
  box-shadow: none;
}
</style>
