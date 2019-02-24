<template>
  <div id="app" class="container">
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
@media only screen and (min-width: 1200px) {
  .container {
    max-width: 960px !important;
  }
}
</style>
