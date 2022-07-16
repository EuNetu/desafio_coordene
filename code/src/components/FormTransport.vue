<template>
  <div>
    <b-form-select v-model="selected" :options="options" size="sm" class="mt-3"></b-form-select>
    <div class="mt-3">Selected: <strong>{{ selected }}</strong></div>
  </div>
</template>

<script>
  import {BFormSelect} from 'bootstrap-vue'

  
  export default {
    components: {
      BFormSelect
    },
    data() {

      return {
        selected: null,
        options: [
          { value: null, text: 'Por favor, selecione a cidade desejada' },
          { value: 'Natal', text: 'Natal' },
          { value: 'Recife', text: 'Recife' },
          { value: 'São Paulo', text: 'São Paulo' },
        ]
      }
    }
  }
</script>

<style>
</style>