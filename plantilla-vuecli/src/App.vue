<template>
  <div class="container mt-3">
    <div class="jumbotron">
      <h1>Ejemplo Parcial</h1>
      <br>
      <Navbar />
      <RouterView />
    </div>
  </div>
</template>
<script>
import Navbar from './components/Navbar.vue';
export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
