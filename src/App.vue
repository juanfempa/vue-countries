<script setup>
import { ref } from 'vue';
const urlApi = 'https://restcountries.com/v3.1/region/europe';

const countries = ref([]);
const countriesAll = ref([]);
const searchText = ref('');
const searchAll = ref(false);

const recuperaCountries = () => {
  fetch(urlApi)
    .then((respuesta) => respuesta.json())
    .then((data) => {
      const paises = data.map(({ name, flags, capital }) => {
        return {
          common: name.common,
          official: name.official,
          alt: flags.alt,
          svg: flags.svg,
          capital: Array.isArray(capital) ? capital[0] : '',
        };
      });
      countries.value = paises;
      countriesAll.value = paises;
    })
    .catch(() => console.log(`Error en la llamada a la API`));
};

const searchCountries = () => {
  countries.value = countriesAll.value.filter((country) => {
    console.log(searchAll.value);
    if (!searchAll.value) {
      return country.common
        .toLowerCase()
        .includes(searchText.value.toLowerCase());
    }
    return `${country.common} ${country.official} ${country.capital}`
      .toLowerCase()
      .includes(searchText.value.toLowerCase());
  });
};

recuperaCountries();
</script>

<template>
  <nav
    class="navbar navbar-expand bg-dark border-bottom border-bottom-dark"
    data-bs-theme="dark"
  >
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Países</a>
      <div class="collapse navbar-collapse">
        <form class="d-flex" role="search">
          <input
            class="form-control me-2"
            type="search"
            placeholder="Buscar"
            aria-label="Buscar"
            v-model="searchText"
            @input="searchCountries"
          />
        </form>
        <div class="form-check form-switch">
          <input
            class="form-check-input"
            type="checkbox"
            role="switch"
            id="flexSwitchCheckChecked"
            v-model="searchAll"
          />
          <label
            class="form-check-label text-bg-dark"
            for="flexSwitchCheckChecked"
            >Buscar en todo</label
          >
        </div>
      </div>
    </div>
  </nav>
  <div class="container">
    <div class="table-responsive-md">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Común</th>
            <th scope="col">Oficial</th>
            <th scope="col">Capital</th>
            <th scope="col">Bandera</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(country, index) in countries">
            <th scope="row" v-text="index + 1"></th>
            <td>{{ country.common }}</td>
            <td>{{ country.official }}</td>
            <td>{{ country.capital }}</td>
            <td>
              <img
                :src="country.svg"
                class="img-thumbnail"
                :alt="country.alt"
              />
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
