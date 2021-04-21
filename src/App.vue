<template>
  <div id="app">
    <meteo></meteo>
  </div>
</template>

<script>
import Meteo from './components/Meteo'

export default {
  name: 'App',
  components: {
    'meteo': Meteo
  }
}

</script>

<style>
body {
 background: linear-gradient(45deg, rgb(155, 71, 71), rgb(56, 117, 128));
  }
</style>
