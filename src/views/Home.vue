<template>
  <section>
    <h1>
      Compre ou venda
    </h1>
    <produto-buscar></produto-buscar>
    <produto-lista></produto-lista>
  </section>
</template>

<script>
import ProdutoBuscar from "../components/ProdutoBuscar.vue";
import ProdutoLista from '../components/ProdutoLista.vue';

export default {
  name: 'Home',
  components: {
    ProdutoBuscar,
    ProdutoLista
  }
}
</script>
<style  scoped>
h1{
  color:#87f;
  margin-top: 40px;
  font-size:2rem;
  text-align: center;
}
</style>