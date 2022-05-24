<template>
  <div>
    <div v-if="products.length > 0" class="products">
      <div
        v-for="(product, index) in products"
        :key="index"
        class="product-card"
        @click="clickProduct(product.id)"
      >
        <img :src="product.image" alt="" />
        <p>{{ product.title }}</p>
        <div class="product-price">
          <p>${{ product.price }}</p>
          <span>{{ product.rating.rate }}</span>
        </div>
      </div>
    </div>
    <div v-else>
      <v-progress-circular indeterminate color="primary"></v-progress-circular>
    </div>

    <!-- <div>{{ $route.params.productId }}</div> -->
  </div>
</template>
<script>
export default {
  data() {
    return {
      products: [],
    };
  },
  methods: {
    clickProduct(id) {
      // console.log(id);
      this.$router.push({ path: `products/${id}`, params: { id: id } });
    },
  },
  async created() {
    // GET request using fetch with async/await
    const response = await fetch("https://fakestoreapi.com/products");
    const data = await response.json();
    // console.log(data);
    this.products = data;
  },
};
</script>

<style>
.products {
  display: flex;
  width: 100vw;
  flex-wrap: wrap;
  padding: 0 2rem;
  justify-content: center;
}
.product-card {
  text-align: center;
  width: 27%;
  border: 2px solid rgba(0, 0, 0, 0.124);
  padding: 2rem;
  margin: 1rem;
  cursor: pointer;
}

.product-card:hover {
  box-shadow: -4px 10px 11px -4px rgba(0, 0, 0, 0.26);
  -webkit-box-shadow: -4px 10px 11px -4px rgba(0, 0, 0, 0.26);
  -moz-box-shadow: -4px 10px 11px -4px rgba(0, 0, 0, 0.26);
}

.product-card img {
  width: 100%;
}
.product-price {
  display: flex;
  justify-content: center;
  margin: 1rem auto;
}
.product-price p {
  font-weight: 700;
  padding: 0 1rem;
}

.product-price span {
  color: rgba(0, 0, 0, 0.549);
}
</style>
