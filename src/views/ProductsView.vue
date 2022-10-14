<template>
  <div class="products-view">
    <div 
      v-for="item in products"
      :key="item.id"
    >
      <span>{{item.title}}</span>
      <span>{{item.price}}$</span>
      <span>{{item.description}}</span>
    </div>
  </div>
</template>
<script>
export default {
  name: 'ProductsView',
  data() {
    return {
      products: null,
    }
  },
  created() {
    fetch(' https://dummyjson.com/products')
      .then((response) => response.json())
      .then(({products}) => {

          this.products = products
      });
  },
};
</script>
<style>

  .products-view span {
    display: block;
  }
    .products-view div {
      margin:  10px auto ;
      width: 300px;
      border: 1px solid black;
  }
</style>