<template>
  <div id="app">
    <crop-image :img-url="imgUrl"></crop-image>
  </div>
</template>

<script>
import CropImage from './components/CropImage.vue'
import Img from './assets/ci.jpeg'
export default {
  name: 'app',
  components: {
    CropImage
  },
  data () {
    return {
      imgUrl: Img
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
