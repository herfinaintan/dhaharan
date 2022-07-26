<template>
<div>
   <b-navbar toggleable="lg" type="light">
      <div class="container">
        <b-navbar-brand href="#">Dhaharan</b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <li class="nav-item">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/menu">Menu</router-link>
            </li>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <li class="nav-item">
              <router-link class="nav-link" to="/keranjang">
                Keranjang
                <b-icon-bag></b-icon-bag>
                <span class="badge badge-success ml-2">0</span>
               
              </router-link>
            </li>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
</div>
</template>

<script>
export default {
  name: "Navigasi-Bar",
};
</script>

<style>
</style>