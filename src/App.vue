<template>
 
  <HelloWorld />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>


<style>
html,
body {
  margin: 0;
  padding: 0;
 
  height: 100%;
  background:darkslategray;
  
}
h1 {
  margin: 0;
  padding: 0;
  color: #c40909;
  
}

ul {
  margin: 0;
}

#app {
  height: 100%;
  
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 2rem;
  height: 100%;
  margin-top:0px;
  background:darkslategray;
  display: flex;
position: relative;
top: 0px;
}

</style>
