<template>
  <div id="app" class="container my-5">
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
}
</style>
