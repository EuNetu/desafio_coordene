<template>
  <div class="container">
    <form id="transport-form">
      <div class="">
        <b-form-select v-model="selectedCity" :options="city" size="sm" class="mt-3">
        </b-form-select>
      </div>
      <div class="b-form-group">
        <b-form-input v-model="peso" placeholder="Insira o peso: "></b-form-input>
        <div class="mt-2">Value: {{ peso }}</div>
      </div>
    </form>
    <b-button type="submit" variant="primary" v-on:click="getBestTransport()">Submit</b-button>
    <div class="mt-3">Cidade Selecionada: <strong>{{ selectedCity }}</strong></div>
  </div>
</template>

<script>
import { BFormSelect } from 'bootstrap-vue'

export default {
  components: {
    BFormSelect
  },
  data() {
    return {
      peso: "",
      selectedCity: "",
      id: null,
      city: [],
      selectTransport: [],
      data: null
    }
  },
  methods: {
    async getTransport() {
      const request = await fetch("http://localhost:3000/transport")
      this.data = await request.json()
      
      this.cities = this.data.map(c => {
        const city = c.city
        return city
      })
      this.city = this.cities.filter((este, i) => this.cities.indexOf(este) === i)
      console.log(this.city)
    },
    async getBestTransport(){
      this.selectTransport = null
      this.transports = this.data.map(c => {
        const transport = c
        return transport
      })
      console.log(this.transports)
      this.selectTransport = this.transports.filter( i => i.city === this.selectedCity)
      console.log(this.selectTransport)
    }
  },
  mounted() {
    this.getTransport()
  }
}
</script>

<style>
</style>