<template>
   <div>
    <p>Pagina {{paginas}}</p>
    <ul>
        <li><router-link :to="{query:{_page:1}}"></router-link></li>    
    </ul>
   </div>     
</template>

<script>

export default ({
   name:"produtos-paginar",
   props:{
       produtos_total:{
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
           let total = this.produtos_total/this.produtos_pagina;
           console.log(total)
           return total
       }
   }
})
</script>

<style>

</style>
