<template>
  <div id="app">
    <POS />
  </div>
</template>


<script>
import POS from './components/POS'
import Vue from 'vue'

Vue.filter('toTHB', function (value) {
    return `฿${value}`;
});

export default {
  name: 'App',
  components: {
    POS
  }
}
</script>

<style>
#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
