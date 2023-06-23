<script setup>
import { ref } from 'vue';
const urlApi = 'https://restcountries.com/v3.1/region/europe';

/**
 * Almacenaremos los países recibidos de la API. Este array se modificará según realizamos las búsquedas.
 */
const countries = ref([]);
/**
 * Creamos una copia de los países que no modificaremos, esta copia ayuda a realizar el filtrado.
 */
const countriesAll = ref([]);
/**
 * Almacenará el texto introducido en el campo de búsqueda.
 */
const searchText = ref('');
/**
 * Indicador que controla si la búsqueda la hacemos en todos los campos o sólo en el de nombre común.
 */
const searchAll = ref(false);

/**
 * Esta función se encarga de recuperar los países y asignarlos a las variables. Respecto a lo visto en clase, se ha añadido la desestructuración para trabajar sólo con los campos utilizados y el catch para controlar posibles errores.
 */
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

/**
 * Se divide en dos tipos, según el tipo de búsqueda deseada. Observar cómo se realiza la búsqueda en (casi) todos los campos.
 */
const searchCountries = () => {
  countries.value = countriesAll.value.filter((country) => {
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
  <!-- Destacar el uso de v-model en la plantilla. -->
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
    <div class="alert alert-danger d-flex align-items-center mt-2" role="alert">
      <div>
        <h4 class="alert-heading">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="32"
            height="32"
            fill="currentColor"
            class="bi bi-exclamation-triangle-fill flex-shrink-0 me-2"
            viewBox="0 0 16 16"
            role="img"
            aria-label="Danger:"
          >
            <path
              d="M8.982 1.566a1.13 1.13 0 0 0-1.96 0L.165 13.233c-.457.778.091 1.767.98 1.767h13.713c.889 0 1.438-.99.98-1.767L8.982 1.566zM8 5c.535 0 .954.462.9.995l-.35 3.507a.552.552 0 0 1-1.1 0L7.1 5.995A.905.905 0 0 1 8 5zm.002 6a1 1 0 1 1 0 2 1 1 0 0 1 0-2z"
            />
          </svg>
          !La aplicación está terminada!
        </h4>
        <p>
          Se han cambiado varias cosas, por favor revisar los comentarios
          añadidos al código fuente. Leer también el
          <span class="fw-bolder">README.md</span> para más detalles y algunos
          apuntes de lo visto estos días.
        </p>
        <hr />
        <p class="mb-0">
          Espero que os esté gustando <span class="fw-bolder">Vue.js</span> y os
          animéis a seguir viendo cosas de él, por vuestra cuenta.
        </p>
      </div>
    </div>
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
