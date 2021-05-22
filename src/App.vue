<template>
  <div id="app">
    
        <cartoon></cartoon>
   
  </div>
  
</template>

<script>

import Cartoon from './components/Cartoon.vue';
export default {
  name: "App",
  components: {
    Cartoon
    
 
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
