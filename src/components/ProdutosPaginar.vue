<template>
   <div>
    <p>Pagina {{paginas}}</p>
    <ul>
        <li v-for="pagina in paginas_total" :key="pagina">
            <router-link :to="{query:{_page:pagina}}">{{pagina}}</router-link>
        </li>
    </ul>
   </div>     
</template>

<script>

export default ({
   name:"produtos-paginar",
   props:{
       paginas_total:{
           type:Number,
           default:1
       },
       produtos_pagina:{
           type:Number,
           default:1
       } 
   },
   computed:{
       paginas(){
           let total = this.paginas_total/this.produtos_pagina;
           return total!==Infinity?Math.ceil(total):0;
       }
   }
})
</script>

<style>

</style>
