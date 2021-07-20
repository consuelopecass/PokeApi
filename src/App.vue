<template>
  <div id="app">
    <pokeguia></pokeguia>
  </div>
</template>

<script>

import PokeGuia from './components/PokeGuia';
export default {
  name: 'App',
  components: {
  "pokeguia": PokeGuia,
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
html {
  background-color: #FCD8D4;
}
</style>
