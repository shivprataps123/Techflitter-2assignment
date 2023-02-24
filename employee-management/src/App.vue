<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <HelloWorld2/>
</template>

<script>
import HelloWorld2 from './components/HelloWorld2.vue'
export default {
  name: 'App',
  components: {
    // HelloWorld,
    HelloWorld2,
   
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;


}
</style>
