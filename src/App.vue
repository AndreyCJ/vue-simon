<template>
  <div id="app">
    <SimonTemplate />
  </div>
</template>

<script>
import SimonTemplate from './components/SimonTemplate.vue'

export default {
  name: 'App',
  components: {
    SimonTemplate
  }
}
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
  font-family: monospace;
  box-sizing: border-box;
  color: #333;
}


button:focus {
  outline: none !important;
}

button::-moz-focus-inner {
  border: 0 !important;
}
</style>
