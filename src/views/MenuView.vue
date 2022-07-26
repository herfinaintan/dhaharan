<template>
  <div>
    <NavigasiBar />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h4>Daftar <strong>Menu</strong></h4>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <input
            v-model="search"
              type="text"
              class="form-control"
              placeholder="Cari Makanan Favoritmu ..."
              aria-label="Cari"
              aria-describedby="basic-addon1"
              @keyup="searchProduct"
            />
            <span class="input-group-text" id="basic-addon1"
              ><b-icon-search></b-icon-search
            ></span>
          </div>
        </div>
      </div>
      <div class="row mb-4">
        <div
          class="col-md-3 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavigasiBar from "@/components/NavigasiBar.vue";
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "MenuView",
  components: {
    NavigasiBar,
    CardProduct,
  },
  data() {
    return {
      products: [],
      search : '',
    };
  },
  methods: {
    setProduct(data) {
      this.products = data;
    },
    searchProduct(){
      axios
      .get("http://localhost:3000/products?q="+this.search)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log("Gagal :  ", error));
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/products")
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log("Gagal :  ", error));
  },
};
</script>

<style>
</style>