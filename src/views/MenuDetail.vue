<template>
  <div class="menu-detail">
    <NavigasiBar />
    <div class="container">
      <!-- breadcrumb -->
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/menu" class="text-dark">Menu</router-link>
              </li>

              <li class="breadcrumb-item active" aria-current="page">
                Pesan Menu
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row mt-3">
        <div class="col md-6">
          <img
            :src="require(`../assets/images/${product.gambar}`)"
            class="img-fluid"
            alt="..."
          />
        </div>
        <div class="col md-6">
          <h3>
            <strong>{{ product.nama }}</strong>
          </h3>
          <h5>
            Harga : <strong> Rp. {{ product.harga }}</strong>
          </h5>
          <form class="mt-4">
            <div class="form-group">
              <label for="jumlah_pemesanan">Jumlah Pesan</label>
              <input type="number" class="form-control" />
            </div>
            <div class="form-group">
              <label for="keterangan">Keterangan</label>
              <textarea
                class="form-control"
                placeholder="Ketrangan seperti : Pedas, Nasi Diperbanyak ..."
              ></textarea>
            </div>
            <button type="submit" class="btn btn-success"><b-icon-cart></b-icon-cart>Pesan</button>
          </form>
        </div>
      </div>
    </div>
    <!-- <h3>Menu Detail {{ $route.params.id }}</h3> -->
  </div>
</template>

<script>
import NavigasiBar from "@/components/NavigasiBar.vue";
import axios from "axios";

export default {
  name: "menuDetail",
  components: {
    NavigasiBar,
  },
  data() {
    return {
      product: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log("Gagal :  ", error));
  },
};
</script>

<style>
</style>