<template>
  <div id="app" >
    <home-page />
  </div>
</template>

<script>
import HomePage from './components/HomePage'

export default {
  name: 'App',
  components: {
    HomePage
  }
}
</script>

<style lang="sass">
$globalFonts: 'Sawarabi Mincho', sans-serif

body
  font-family: $globalFonts

</style>

