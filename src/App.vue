<template>
  <div id="app">
    <img id="banner" src="./assets/logo.png">
    <v-app>
      <HomePage></HomePage>
    </v-app>
  </div>
</template>

<script>
import HomePage from '@/components/HomePage'

export default {
  name: 'App',
  components: {
    HomePage
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#banner {
  height: 50px
}

</style>
