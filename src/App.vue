<script setup>
import { ref } from 'vue'
const urlApi = 'https://restcountries.com/v3.1/region/europe'

function recuperaCountries() {
  fetch(urlApi)
    .then((respuesta) => respuesta.json())
    .then((data) => {
      console.log(data)
      countries.value = data
    })
}

recuperaCountries();

const countries = ref([])
</script>

<template>
  {{ countries }}
</template>