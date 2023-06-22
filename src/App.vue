<script setup>
import { ref } from 'vue';
const urlApi = 'https://restcountries.com/v3.1/region/europe';

function recuperaCountries() {
  fetch(urlApi)
    .then((respuesta) => respuesta.json())
    .then((data) => {
      console.log(data);
      countries.value = data;
    });
}

recuperaCountries();

const countries = ref([]);
const isPrimary = ref(false);
const isDanger = ref(true);

const toggleButton = () => {
  isPrimary.value = !isPrimary.value;
  isDanger.value = !isDanger.value;
};
</script>

<template>
  <button
    type="button"
    class="m-2 btn"
    @click="toggleButton"
    :class="{
      'btn-primary': isPrimary,
      'btn-danger': isDanger,
    }"
  >
    MI LISTA
  </button>
</template>
