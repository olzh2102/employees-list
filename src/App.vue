<template>
  <div id="app">
    <Navbar />
    <div class="container">
      <router-view/>
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar'

export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>
body {
  font-family: 'Molengo', sans-serif;
  background: #A1A6B4;
}
.container {
  max-width: 1000px;
}
</style>
