<template>
  <div id="app">
    <Headers>
    </Headers>
    <HelloWorld msg="Dogs World"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
//import Headers from './components/Headers.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Headers
  }
}
</script>

<style>
body{
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
/*  margin-top: 60px;*/
}
</style>
