<template>
  <div class="pesanan-sukses">
    <NavigasiBar />
      <div class="container">
        <div class="row justify-content-center mt-5">
            <div class="col text-center">
               <img src="../assets/images/menunggu.png" width="300" />
              <h4><strong>Sukses !!</strong></h4>
              <h6>Pesanan Anda segera diproses <br> Mohon Menunggu</h6>
            </div>
        </div>
      </div>
  </div>
</template>

<script>
import NavigasiBar from "@/components/NavigasiBar.vue";
export default {
  components: {
    NavigasiBar,
  },
};
</script>

<style>
</style>