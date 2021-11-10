<template>
  <div class="h-100" id="app">
    <Header/>

    <PhotoGrid/>
  </div>
</template>

<script>
import PhotoGrid from './components/PhotoGrid.vue'
import Header from './components/Header.vue'

export default {
  name: 'App',
  components: {
    PhotoGrid,
    Header,
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
