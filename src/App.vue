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


/*for FireFox*/
input[type="submit"]::-moz-focus-inner, input[type="button"]::-moz-focus-inner
{   
  border : 0;
} 
/*for IE8 and below */
input[type="submit"]:focus, input[type="button"]:focus
{     
  outline : none; 
}

.no-pointer {
  pointer-events: none;
}
</style>
