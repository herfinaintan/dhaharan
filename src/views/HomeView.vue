<template>
  <div class="home">
    <NavigasiBar />
    <div class="container">
      <Hero />
      <div class="row mt-4">
        <div class="col">
          <h3>Menu <strong>Favorit</strong></h3>
        </div>
        <div class="col">
          <router-link to="/menu" class="btn btn-success float-right"
            ><b-icon-eye></b-icon-eye>Lihat Semua</router-link
          >
        </div>
      </div>
      <div class="row mb-4">
        <div class="col-md-3 mt-4" v-for="product in products" :key="product.id">
          <CardProduct :product="product"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import NavigasiBar from "@/components/NavigasiBar.vue";
import Hero from "@/components/Hero.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    NavigasiBar,
    Hero,
    CardProduct,
  },
  data() {
    return {
      products: [],
    };
  },
  methods: {
    setProduct(data) {
      this.products = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/best-products")
      .then((response) => this.setProduct(response.data))
      .catch( (error) =>console.log("Gagal :  ",error))
  },
};
</script>
