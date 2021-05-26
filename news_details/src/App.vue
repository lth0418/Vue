<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3.0 + Vite" /> -->
  <Home/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Home from './views/Home.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Home
  }
}
</script>
