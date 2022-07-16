<template>
  <div class="container">
    <form id="transport-form">
      <div class="">
        <b-form-select v-model="selectedCity" :options="city" size="sm" class="mt-3">
        </b-form-select>
      </div>
      <div class="b-form-group">
        <b-form-input v-model="peso" placeholder="Insira o peso: "></b-form-input>
      </div>
    </form>
    <b-button type="submit" variant="primary" v-on:click="getBestTransport()">Submit</b-button>
      <div class="mt-3">A Transportadora mais barata para sua entrega é a:
        <strong>{{ this.transportMenorValor.name }}</strong>
      </div>
      <div class="mt-2">No valor de:
        <strong>R${{ this.menorValorFinal }}</strong>
      </div>
      <div class="mt-3">A Transportadora mais rápida para sua entrega é a:
        <strong>{{ this.transportMenorTempo.name }}</strong>
      </div>
      <div class="mt-2">O tempo de entrega é de:
        <strong>{{ this.menorTempoFinal }}hr</strong>
      </div>
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
      carga: "",
      city: [],
      selectTransport: [],
      data: null,
      menorValor: "",
      transportMenorValor: [],
      menorTempo: "",
      transportMenorTempo: [],
      menorValorFinal: "",
      menorTempoFinal: ""
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
    async getBestTransport() {
      this.selectTransport = null
      this.transports = this.data.map(c => {
        const transport = c
        return transport
      })
      console.log(this.transports)
      this.selectTransport = this.transports.filter(i => i.city === this.selectedCity)
      console.log(this.selectTransport)


      const peso = Number(this.peso)
      var i = 0
      if (peso >= 100) {
        this.transportMenorValor = null
        this.menorValor = Number(this.selectTransport[i].cost_transport_heavy.slice(3))
        this.transportMenorValor = this.selectTransport[i]
        for (i = 0; i < this.selectTransport.length; i++) {
          console.log(Number(this.selectTransport[i].cost_transport_heavy.slice(3)))
          if (Number(this.selectTransport[i].cost_transport_heavy.slice(3)) < this.menorValor) {
            this.menorValor = Number(this.selectTransport[i].cost_transport_heavy.slice(3))
            this.transportMenorValor = this.selectTransport[i]
          }
        }
      } else {
        this.transportMenorValor = null
        this.menorValor = Number(this.selectTransport[i].cost_transport_light.slice(3))
        this.transportMenorValor = this.selectTransport[i]
        for (i = 0; i < this.selectTransport.length; i++) {
          console.log(Number(this.selectTransport[i].cost_transport_light.slice(3)))
          if (Number(this.selectTransport[i].cost_transport_light.slice(3)) < this.menorValor) {
            this.menorValor = Number(this.selectTransport[i].cost_transport_light.slice(3))
            this.transportMenorValor = this.selectTransport[i]
          }
        }


      }
      console.log(this.transportMenorValor)


      i = 0
      this.transportMenorTempo = null
      this.menorTempo = Number(this.selectTransport[i].lead_time.slice(0, -1))
      for (i = 0; i < this.selectTransport.length; i++) {
        console.log(Number(this.selectTransport[i].lead_time.slice(0, -1)))
        console.log(this.menorTempo)
        if (Number(this.selectTransport[i].lead_time.slice(0, -1)) <= this.menorTempo) {
          this.menorTempo = Number(this.selectTransport[i].lead_time.slice(0, -1))
          this.transportMenorTempo = this.selectTransport[i]
        }
      }
      console.log(this.transportMenorTempo)
      this.menorValor = this.menorValor*peso
      this.menorTempoFinal = this.menorTempo.toString()
      this.menorValorFinal = this.menorValor.toString()
    }
  },
  mounted() {
    this.getTransport()
  }
}
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

#transport-form {
  margin-bottom: 10px;
}

b-form-input {
  margin-top: 10px;
}

.mt-3 {
  display: flex;
  align-items: center
}
</style>