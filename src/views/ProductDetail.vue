<template>
  <button @click="router.push({ name: 'Catalog' })">Back to catalog</button>
  <div class="product">
    <div class="product-image">
      <img :src="selectedProduct.thumbnail" alt="">
    </div>
    <div class="product-details">
      <p>Brand: {{ selectedProduct.brand }}</p>
      <p>Description: {{ selectedProduct.description }}</p>
      <h2>Price: ${{ selectedProduct.price }}</h2>
      <button @click="addToCart">Add to cart</button>
    </div>
  </div>
</template>


<script>
  import { defineComponent } from "vue";
  export default defineComponent({
    name: 'ProductDetails'
  })
</script>

<script setup>
  import { computed } from "vue";
  import { productsStore } from "@/stores/products";
  import { useRoute, useRouter } from "vue-router";

  const store = productsStore()
  const router = useRouter()
  const route = useRoute()

  const selectedProduct = computed(() => {
    return store.products.find((item) => item.id === Number(route.params.id))
  })

  const addToCart = () => {
    store.addToCart(selectedProduct.value)
    router.push({ name: 'CartView' })
  }
</script>

<style scoped>
.product {
  display: flex;
  margin-top: 50px;
}

.product-image {
  margin-right: 24px;
}

</style>