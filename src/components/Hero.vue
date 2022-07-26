<template>
  <!--desktop-->
  <div class="hero">
    <div class="d-none d-md-block">
      <div class="row mt-4">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h3>
                Menu Dhaharan, <br />
                <strong>Citra Rasa Khas Jawa </strong>
              </h3>
              <p>Ayo pilih dan pesan menu favorit Anda</p>
              <router-link class="btn btn-lg btn-success" to="/menu"
                ><b-icon-arrow-right></b-icon-arrow-right>Pesan</router-link
              >
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <div class="img img-hero">
            <img src="../assets/images/ilustrasi.png" width="100%" />
          </div>
        </div>
      </div>
    </div>
    <!--mobile-->
    <div class="d-sm-block d-md-none">
      <div class="row mt-4">
        <div class="col-md-6 mb-3">
          <div class="img img-hero">
            <img src="../assets/images/ilustrasi.png" width="100%" />
          </div>
        </div>
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h3>
                Menu Dhaharan, <br />
                <strong>Citra Rasa Khas Jawa </strong>
              </h3>
              <p>Ayo pilih dan pesan menu favorit Anda</p>
              <router-link class="btn btn-lg btn-success" to="/menu"
                ><b-icon-arrow-right></b-icon-arrow-right>Pesan</router-link
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Hero-Component",
};
</script>

<style>
</style>