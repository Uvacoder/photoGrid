<template>
  <div id="app">
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
    Header,
    PhotoGrid,
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
}
</style>
