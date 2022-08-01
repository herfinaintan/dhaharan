<template>
  <div class="keranjang">
    <NavigasiBar :updateKeranjang="keranjangs" />
    <div class="container">
      <!-- breadcrumb -->
      <div class="row mt-4">
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
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h5>Keranjang <strong>Saya</strong></h5>
          <div class="table-responsive mt-3">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Gambar</th>
                  <th scope="col">Menu</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">Jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th>{{ index + 1 }}</th>
                  <!-- desktop -->
                  <div class="d-none d-md-block">
                    <td>
                      <img
                        :src="
                          require(`../assets/images/${keranjang.products.gambar}`)
                        "
                        class="img-keranjang-dekstop"
                        alt="..."
                      />
                    </td>
                  </div>
                  <!-- mobile -->
                  <div class="d-sm-block d-md-none">
                    <td>
                      <img
                        :src="
                          require(`../assets/images/${keranjang.products.gambar}`)
                        "
                        class="img-keranjang"
                        alt="..."
                      />
                    </td>
                  </div>
                  <td>
                    <strong>{{ keranjang.products.nama }}</strong>
                  </td>
                  <td>
                    {{ keranjang.keterangan ? keranjang.keterangan : "-" }}
                  </td>
                  <td>{{ keranjang.jumlah_pemesanan }}</td>
                  <td align="right">{{ keranjang.products.harga }}</td>
                  <td align="right">
                    <strong>
                      {{
                        keranjang.products.harga * keranjang.jumlah_pemesanan
                      }}</strong
                    >
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash
                      @click="hapusKeranjang(keranjang.id)"
                    ></b-icon-trash>
                  </td>
                </tr>
                <tr>
                  <td colspan="6" align="right">
                    <strong>Total Harga :</strong>
                  </td>
                  <td align="right">
                    <strong>Rp. {{ totalHarga }}</strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      <!-- Form Checkout -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="nama">Nama :</label>
              <input type="text" class="form-control" v-model="pesan.nama" />
            </div>
            <div class="form-group">
              <label for="noMeja">Nomor Meja :</label>
              <input type="number" class="form-control" v-model="pesan.noMeja" />
            </div>
            <button type="submit" class="btn btn-success" @click="checkout">
              <b-icon-cart></b-icon-cart>Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavigasiBar from "../components/NavigasiBar.vue";
import axios from "axios";

export default {
  components: { NavigasiBar },
  name: "keranjangView",
  data() {
    return {
      keranjangs: [],
      pesan: {},
    };
  },
  methods: {
    setKeranjang(data) {
      this.keranjangs = data;
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        .then(() => {
          this.$toast.error("Sukses Menghapus Keranjang", {
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });

          // Update Data Keranjang
          axios
            .get("http://localhost:3000/keranjangs/")
            .then((response) => this.setKeranjang(response.data))
            .catch((error) => console.log("Gagal :  ", error));
        })
        .catch((error) => console.log("Gagal :  ", error));
    },
    checkout(){
      if(this.pesan.nama && this.pesan.noMeja){
        this.pesan.keranjangs = this.keranjangs;
        axios
          .post("http://localhost:3000/pesanans", this.pesan)
          .then(() => {
            // Hapus semua keranjang
            this.keranjangs.map(function(item){
              return axios
                .delete("http://localhost:3000/keranjangs/"+item.id)
                .catch((error)=>console.log(error));
            })

            this.$router.push({ path: "/pesanan-sukses"});
            this.$toast.success("Sukses Dipesan", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
      }else{
        {
          this.$toast.error("Nama dan No.Meja Harus Diisi", {
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });
        }
      }
    }
  },
  mounted() {
    axios
      .get("http://localhost:3000/keranjangs/")
      .then((response) => this.setKeranjang(response.data))
      .catch((error) => console.log("Gagal :  ", error));
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(function (items, data) {
        return items + data.products.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>

<style>
</style>