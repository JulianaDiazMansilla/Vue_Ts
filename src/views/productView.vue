<template>
    <div class="product">
      <h2 v-if  = "isLoading"> Espere un poco</h2>
      <h2 v-else>Productos</h2>
    </div>

    <div   v-if ="products.length > 0">
      <ul class = "container">
          <li class = "user-list" v-for="{id, title, price, images} in products" :key = "id">
            <h4>{{ title  }}</h4>
            <!--<h4>{{ description  }}</h4>-->
            <h4>{{ price  }}</h4>  
            <img class="product-image" :src="images" :alt="images" />
          </li>
          
    </ul>


    </div>
</template>

<script lang ='ts'>

import { ref } from 'vue'
import axios from 'axios'

export default {

  setup() {

    const products = ref ([])
    const isLoading = ref(true)

    const getUsers = async () => {

    

      isLoading.value = true

      const resp = await axios.get('https://api.escuelajs.co/api/v1/products', )

      console.log(resp.data)
      isLoading.value = false
      products.value = resp.data
      

      

    }
    getUsers()

    return { 
        products,
        isLoading,


    }
  }
}
</script>

<style scoped>
.user-list {
  
  display: flex;
  flex-wrap: nowrap;
  width: 100%;
  gap: 1rem 1rem;
  width: 300px;
  border-style: solid;
}
.product-image {

  width: 150px;
  ;
}

.container {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  gap: 1rem 1rem;

}
</style>