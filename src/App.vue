<template>
  <div id="app">
    <painter></painter>
  </div>
</template>

<script>
import Painter from '/src/components/Painter'
export default {
  name: 'App',
  components: {
    Painter : Painter
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
