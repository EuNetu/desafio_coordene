<template>
    <div class="title">
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand class="ml-2">
        <img class="logo" src="../assets/logo.png"/>
        <b>{{ appName }}</b>
      </b-navbar-brand>
    </b-navbar>
  </div>

</template>

<script>
import {
  BNavbar,
  BNavbarBrand,
} from 'bootstrap-vue'

export default {
  name: 'NavbarTransporte',
  components: {
    BNavbar,
    BNavbarBrand,
  },
  data() {
    const appName = ''

    return {
      appName,
    }
  },
  created() {
    // Implemente aqui o GET dos dados da API REST
    // para que isso ocorra na inicialização da pagina
    this.appName = 'Melhor Frete'
  },
  methods: {
    // Implemente aqui os metodos utilizados na pagina
    methodFoo() {
      console.log(this.appName)
    },
  },
}
</script>

<style scoped>
.title .logo {
  width: 100px;
  margin: 0 30px 0 50px;
}
.title .navbar {
  background-color: #00aca6 !important;
}

.title .navbar-brand {
  margin-left: 20px;
}
b{
  margin-top: 40px;
  font-size: 40px;
  text-shadow: 2px 2px 8px rgb(80, 79, 79);
}
</style>
