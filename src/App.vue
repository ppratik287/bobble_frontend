<template>
  <div id="app">
      <Login></Login>
  </div>
</template>

<script>
import Login from './components/Login'
export default {
  name: 'App',
  components: {
    Login,
  }
}
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #343a40;
  /* margin-top: 60px; */
  overflow-x:hidden
}
</style>
