<template>
  <!-- <div>detailed product {{ $route.params.productId }}</div> -->
  <div>
    <div class="detail" v-if="detail.id == this.$route.params.productId">
      <div class="detail-image">
        <img :src="detail.image" />
      </div>
      <div class="detail-details">
        <h1>{{ detail.title }}</h1>
        <p>{{ detail.description }}</p>
        <div class="price-button">
          <h3>${{ detail.price }}</h3>
          <v-btn class="ma-2" outlined color="indigo" @click="addToCart">
            Add to Cart
          </v-btn>
        </div>
      </div>
    </div>
    <div v-else>
      <v-progress-circular indeterminate color="primary"></v-progress-circular>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      detail: [],
    };
  },
  methods: {
    addToCart() {
      this.$router.push({ path: "/cart" });
    },
  },
  async created() {
    // GET request using fetch with async/await
    const response = await fetch(
      `https://fakestoreapi.com/products/${this.$route.params.productId}`
    );
    const data = await response.json();
    // console.log(data);
    this.detail = data;
  },
};
</script>
<style>
.detail {
  display: flex;
  justify-content: center;

  width: 100vw;
}

.detail-image {
  width: 30%;
}
.detail-image img {
  width: 100%;
}

.detail-details {
  text-align: left;
  width: 50%;
  padding: 0 2rem;
}

.price-button {
  margin-top: 1rem;
  display: flex;
  align-items: center;
}
.price-button h3 {
  padding: 0 1rem 0 0;
}
</style>
