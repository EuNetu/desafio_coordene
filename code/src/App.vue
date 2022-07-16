<template>
  <div id="app">
    <NavbarTransporte/>
    <BestTransport/>
    <FormTransport/>
  </div>
</template>

<script>
import BestTransport from './components/BestTransport.vue'
import FormTransport from './components/FormTransport.vue'
import NavbarTransporte from './components/Navbar.vue'

export default {
  name: 'App',
  components: {
    BestTransport,
    FormTransport,
    NavbarTransporte,
  }
}
</script>

<style>
</style>
