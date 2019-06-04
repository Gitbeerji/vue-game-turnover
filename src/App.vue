<template>
  <div class="wrap">
      <router-view/>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: 'App'
}
</script>

<style>
html {
    box-sizing: border-box;
}
*,
*::before,
*::after {
    box-sizing: border-box;
}
html,
body {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
}
body {
    background-size: 100% auto;
}
#app {
  font-family:  Arial, sans-serif, 'Avenir', Helvetica;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.wrap {
  position: relative;
  max-width: 600px;
  margin: 0 auto;
  background: #FFF;
}
h1 {
  font-family: 'Open Sans', sans-serif;
  font-weight: 300;
}

img, div, span, a, button, input {
	-webkit-tap-highlight-color: rgba(0,0,0,0);
  -webkit-tap-highlight-color: transparent;
  outline: 0;
}
</style>
