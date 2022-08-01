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
      <!-- desktop -->
      <div class="d-none d-md-block">
        <div class="row mt-3">
          <div class="col md-6">
            <img
              :src="require(`../assets/images/${product.gambar}`)"
              class="img"
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
            <form class="mt-4" v-on:submit.prevent>
              <div class="form-group">
                <label for="jumlah_pemesanan">Jumlah Pesan</label>
                <input
                  type="number"
                  class="form-control"
                  v-model="pesan.jumlah_pemesanan"
                />
              </div>
              <div class="form-group">
                <label for="keterangan">Keterangan</label>
                <textarea
                  v-model="pesan.keterangan"
                  class="form-control"
                  placeholder="Keterangan seperti : Pedas, Nasi Diperbanyak ..."
                ></textarea>
              </div>
              <button type="submit" class="btn btn-success" @click="pemesanan">
                <b-icon-cart></b-icon-cart>Pesan
              </button>
            </form>
          </div>
        </div>
      </div>
      <!-- mobile -->
      <div class="d-sm-block d-md-none">
        <div class="row mt-3">
          <div class="col-md-6 ">
            <img
              :src="require(`../assets/images/${product.gambar}`)"
              class="img"
              alt="..."
            />
          </div>
          <div class="col-md-6 mt-5">
            <h3>
              <strong>{{ product.nama }}</strong>
            </h3>
            <h5>
              Harga : <strong> Rp. {{ product.harga }}</strong>
            </h5>
            <form class="mt-4" v-on:submit.prevent>
              <div class="form-group">
                <label for="jumlah_pemesanan">Jumlah Pesan</label>
                <input
                  type="number"
                  class="form-control"
                  v-model="pesan.jumlah_pemesanan"
                />
              </div>
              <div class="form-group">
                <label for="keterangan">Keterangan</label>
                <textarea
                  v-model="pesan.keterangan"
                  class="form-control"
                  placeholder="Keterangan seperti : Pedas, Nasi Diperbanyak ..."
                ></textarea>
              </div>
              <button type="submit" class="btn btn-success" @click="pemesanan">
                <b-icon-cart></b-icon-cart>Pesan
              </button>
            </form>
          </div>
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
      pesan: {},
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({ path: "/keranjang" });
            this.$toast.success("Berhasil Masuk Keranjang", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Jumlah Pesanan Harus Diisi", {
          type: "error",
          position: "top-right",
          duration: 3000,
          dismissible: true,
        });
      }
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