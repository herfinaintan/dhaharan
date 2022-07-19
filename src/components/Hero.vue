<template>
  <div class="row mt-2">
    <div class="col">
      <div class="d-flex h-100">
        <div class="slogan justify-content-center align-self-center">
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
    <div class="col">
      <div class="img img-hero">
        <img src="../assets/images/hero.png" width="100%" />
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