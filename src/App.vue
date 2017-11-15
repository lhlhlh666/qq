<template>
  <div id="app">  
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* max-width: 1920px; */
  
  /* margin-top: 60px; */
}
.clearfix::after {
  content: "";

  display: block;

  clear: both;

  height: 0px;

  overflow: hidden;
}

.clearfix {
  -ms-zoom: 1;
}
*{
  margin: 0;
  padding: 0;
  
}
</style>
