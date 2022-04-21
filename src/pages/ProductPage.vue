<template>
    <div>
       <ListProduct :data="product" />
    </div>
</template>
<script>
import ListProduct from '../components/ListProduct.vue'
import product from '../assets/json/product.json'
export default {
    name: 'ProductPage',
    data(){
    return{      
      product: product
    }
  },
  components: {    
    ListProduct
  }
}
</script>
