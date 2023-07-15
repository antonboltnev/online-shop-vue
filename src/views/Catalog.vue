<template>
  <div class="products-list">
    <v-text-field clearable label="Label" prepend-icon="$vuetify"></v-text-field>
    <v-row no-gutters>
      <v-col
          v-for="product in store.products"
          :key="product.id"
          cols="12"
          sm="4"
          @click="goToProductPage(product.id)"
      >
        <v-sheet class="ma-2 pa-2">
          <v-card
              class="product"
          >
            <v-img
                :src="product.thumbnail"
                height="200px"
                cover
            />

            <v-card-title>
              {{ product.brand }}
            </v-card-title>

            <v-card-subtitle>
              $ {{ product.price }}
            </v-card-subtitle>

            <v-card-text>
              {{ product.description }}
            </v-card-text>

            <v-card-actions>
              <v-btn @click="goToProductPage(product.id)">
                Add to cart
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-sheet>
      </v-col>
    </v-row>

    </div>
</template>

<script>
  import { defineComponent } from "vue";
  export default defineComponent({
    name: 'CatalogView'
  })
</script>

<script setup>
  import { onMounted, ref } from "vue";
  import { productsStore } from "@/stores/products";
  import { useRouter } from "vue-router";

  const store = productsStore()
  const router = useRouter()

  const search = ref('')

  const goToProductPage = (id) => {
    router.push({ name: 'ProductView', params: { id } })
  }


  onMounted(async () => {
    await store.fetchProductsFromDB()
  })
</script>

<style scoped>

</style>