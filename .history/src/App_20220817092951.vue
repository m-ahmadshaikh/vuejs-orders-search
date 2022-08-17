<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>


<style scoped>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  
}
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
h1,h2,h3,h4,h5,h6{
  color: #fff;
}
</style>
