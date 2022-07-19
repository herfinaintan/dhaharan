<template>
  <div class="home">
    <NavigasiBar/>
    <div class="container">
      <Hero/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import NavigasiBar from '@/components/NavigasiBar.vue'
import Hero from '@/components/Hero.vue'

export default {
  name: 'HomeView',
  components: {
    NavigasiBar,
    Hero,
  }
}
</script>
