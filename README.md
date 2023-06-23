# vue-countries

Esta plantilla debería ayudarlo a comenzar a desarrollar con Vue 3 en Vite.

## Configuración IDE recomendada

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (y desactivar Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Personalizar configuración

Consulte [Referencia de configuración de Vite](https://vitejs.dev/config/).

## Configuración del proyecto

```sh
npm install
```

### Compilar y recargar en caliente para el desarrollo

```sh
npm run dev
```

### Compilar y Minificar para Producción

```sh
npm run build
```

# Apuntes

## Git - Etiquetas

[Etiquetas](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Etiquetado#r_git_tagging).
Las etiquetas se usan para marcar versiones de código para lanzamiento.

### Listar Etiquetas

Para listar las etiquetas disponibles en Git, simplemente escribe:

```sh
$ git tag
v0.1
v1.3
```

### Etiquetas Anotadas

Para crear una etiqueta anotada, la forma más fácil de hacerlo es especificar la opción -a cuando ejecutas el comando git tag:

```sh
$ git tag -a v1.4 -m 'my version 1.4'
$ git tag
v0.1
v1.3
v1.4
```

### Compartir Etiquetas

Por defecto, el comando git push no transfiere las etiquetas a los servidores remotos. Debes enviar las etiquetas de forma explícita al servidor luego de que las hayas creado. Este proceso es similar al de compartir ramas remotas - puedes ejecutar git push origin [etiqueta].

```sh
$ git push origin v1.5

Counting objects: 14, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (12/12), done.
Writing objects: 100% (14/14), 2.05 KiB | 0 bytes/s, done.
Total 14 (delta 3), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.5 -> v1.5
```

Si quieres enviar varias etiquetas a la vez, puedes usar la opción --tags del comando git push. Esto enviará al servidor remoto todas las etiquetas que aun no existen en él.

```sh
$ git push origin --tags

Counting objects: 1, done.
Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
 * [new tag]         v1.4 -> v1.4
 * [new tag]         v1.4-lw -> v1.4-lw
```

Por lo tanto, cuando alguien clone o traiga información de tu repositorio, también obtendrá todas las etiquetas.

---

# RESUMEN

```sh
$ git tag
$ git tag -a v0.1 -m 'versión inicial'
$ git push origin --tags
```

---

# Vue.js

## Crear App-vue y limpiar

```sh
cd "directorio de trabajo"
npm init vue@latest
cd "app-vue"
npm install
git init
code .

```

## Vemos la interpolación

```php
{{ 1 + 1 }}
```

## Repasamos _data_ y _methods_

Descubrimos el nuevo:

```js
<script setup>
```

## Añadir Array de frases y mostrarlas en duro

Sacadas de [proverbia.net](https://proverbia.net/)

```js
const frases = [
  {
    frase:
      'La más bella palabra en labios de un hombre es la palabra madre, y la llamada más dulce: madre mía.',
    autor: 'Khalil Gibran (1883-1931) Ensayista, novelista y poeta libanés.',
    tema: 'madres',
  },
  {
    frase: 'Hay un solo niño bello en el mundo y cada madre lo tiene.',
    autor: 'José Martí (1853-1895) Político y escritor cubano.',
    tema: 'madres',
  },
  {
    frase:
      'A una madre se la quiere siempre con igual cariño y a cualquier edad se es niño cuando una madre se muere.',
    autor: 'José María Pemán (1898-1981) Escritor español.',
    tema: 'madres',
  },
  {
    frase: 'El porvenir de un hijo es siempre obra de su madre.',
    autor: 'Napoleón I (1769-1821) Napoleón Bonaparte. Emperador francés.',
    tema: 'madres',
  },
  {
    frase:
      'Jamás en la vida encontraréis ternura mejor y más desinteresada que la de vuestra madre.',
    autor: 'Honoré de Balzac (1799-1850) Escritor francés.',
    tema: 'madres',
  },
  {
    frase: 'Las madres perdonan siempre: han venido al mundo para eso.',
    autor: 'Alejandro Dumas (1802-1870) Escritor francés.',
    tema: 'madres',
  },
  {
    frase: 'La mano que mece la cuna rige el mundo.',
    autor: 'Peter de Vries (1910-1993) Editor y novelista estadounidense.',
    tema: 'madres',
  },
  {
    frase: 'Quien quiere a su madre no puede ser malo.',
    autor: 'Alfred de Musset (1810-1857) Poeta francés.',
    tema: 'madres ',
  },
  {
    frase:
      'Todo lo que soy o espero ser se lo debo a la angelical solicitud de mi madre.',
    autor: 'Abraham Lincoln (1808-1865) Político estadounidense.',
    tema: 'madres',
  },
  {
    frase: 'La mano que mece la cuna es la mano que gobierna el mundo.',
    autor: 'William Ross Wallace (1819-1892) Poeta estadounidense.',
    tema: 'madres',
  },

  {
    frase:
      'El corazón de una madre es un abismo en el fondo del cual siempre hay un perdón.',
    autor: 'Honoré de Balzac (1799-1850) Escritor francés.',
    tema: 'madres',
  },
  {
    frase:
      '¿Cómo no amarte, madre, si me enseñaste a hablar tu lengua? ¿Si soy viento nacido de tu roca?',
    autor: 'Gonzalo Rojas (1916-2011) Profesor y periodista chileno.',
    tema: 'madres',
  },
  {
    frase:
      'Muchas maravillas hay en el universo; pero la obra maestra de la creación es el corazón materno.',
    autor: 'Ernest Bersot (1816-1880) Filósofo francés.',
    tema: 'madres',
  },
];
```

## Directiva _v-for_

Mostrarlas con v-for (con in, no se suele usar of)

```html
<ul>
  <li v-for="frase in frases">{{ frase }}</li>
</ul>
```

## Enseñar la desestructuración

```js
let a, b;
const objeto = { a: 1, b: 2 };

({ a, b } = objeto);
```

## Recordamos etiqueta HTML para frases

```html
<blockquote>— Este guión largo se introduce con: ALT+0151</blockquote>
```

## Más sobre _v-for_

Esta directiva también nos proporciona el INDEX

- Ejercicio:

  Desestructurar con índice incluido

- Solución:

  ```html
  <li v-for="({ frase, autor }, index) in frases"></li>
  ```

## Eventos

Enseñamos la directiva para los eventos: **v-on:evento** y su forma reducida **@:evento**

```html
<input type="text" v-on:keypress="" />
```

## Funciones de flecha

Repaso funciones de flecha

- Ejercicio:

  Transformar la función siguiente a una de flecha:

  ```js
  function miFuncion() {
    console.log('Hola mundo');
  }
  ```

- Solución:

  ```js
  const miFuncion = () => {
    console.log('Hola mundo');
  };
  ```

## Repaso argumento _Event_

Recordar que los eventos HTML nos mandan un objeto _Event_ que podemos usar o no según nuestras necesidades.

## Directiva de doble enlace

**V-MODEL** (se usa principalmente en etiqueta input)

## Elementos reactivos

Uso de **ref()**. Recordar que hay que traerlo de la librería _vue_:

```js
import { ref } from 'vue';
```

Enseñamos que en la sección de `<script setup></script>` es imprescindible usar la propiedad **value**:

```js
const frases = ref('En un lugar de la Mancha');
frases.value = 'de cuyo nombre no quiero acordarme';
```

- Ejercicio:

  Añadir frases _al pulsar enter_

- Solución:

Los eventos admiten [modificadores](https://vuejs.org/guide/essentials/event-handling.html#event-modifiers), uno de ellos es **.enter**

```html
<input type="text" v-on:keypress.enter="" />
```

- Ejercicio:

  Añadir frase al principio

- Solución:

  Esto es [sólo un ejemplo](https://www.elmundo.es/comunidad-valenciana/2015/10/28/5630928bca4741a11f8b4585.html):

  ```js
  frases.value = frases.value.unshift({
    frase: 'Mi mamá me mima.',
    autor: 'Cuadernos Rubio.',
    tema: 'madres',
  });
  ```

## Enseñamos otro modificadores

Vemos que hay varios y que estos se pueden **encadenar**

```js
@keyup.alt.enter
```

También vemos que con ellos no necesitamos pasar el objeto Event

## Directiva condicional

- V-IF
- V-SHOW

Vemos también el código que añade vue

## Problemas si los usamos juntos V-FOR y V-IF

Ver la [guía de estilos](https://vuejs.org/style-guide/)

# Instalar PRETTIER y ESLINT

## PRETTIER

Ver la web oficial de [Prettier](https://prettier.io/docs/en/install.html).

```sh
npm install --save-dev --save-exact prettier
```

Archivo de configuración:

```sh
.prettierrc.json
```

Le añadimos los siguientes valores:

```json
{
  "singleQuote": true,
  "semi": false,
  "arrowParens": "avoid",
  "endOfLine": "lf",
  "printWidth": 80,
  "tabWidth": 2,
  "trailingComma": "all"
}
```

## ESLINT

Visitar la web oficial de [Eslint](https://eslint.vuejs.org/).

```sh
npm install --save-dev eslint eslint-plugin-vue
```

Archivo de configuración:

```sh
.eslintrc.js
```

Le añadimos los siguientes valores:

```js
module.exports = {
  env: {
    node: true,
    // Añadir si falla el defineProps()
    //'vue/setup-compiler-macros': true,
  },
  extends: [
    // add more generic rulesets here, such as:
    'eslint:recommended',
    'plugin:vue/vue3-recommended',
    // 'plugin:vue/recommended' // Use this if you are using Vue.js 2.x.
    'prettier',
  ],
  rules: {
    // override/add rules settings here, such as:
    // 'vue/no-unused-vars': 'error'
  },
};
```

## ESLINT && PRETTIER

Hay ocasiones en los que ambos sistemas chocan al tratar de hacer su trabajo, para ello se creó esta librería que trata de configurarlos de modo que no se produzcan esos choques:

[eslint-config-prettier](https://www.npmjs.com/package/eslint-config-prettier)

```sh
npm install --save-dev eslint-config-prettier
```

## Configurar "scripts"

Podemos añadir las siguientes líneas a la sección **scripts** de nuestro archivo **package.json** para lanzar las utilidades desde la línea de comandos:

```json
"scripts": {
	...
	"lint": "eslint --ext .js,.vue --ignore-path .gitignore --fix src"
	"format": "prettier . --write"
},
```

---

# Aplicación Trivial

## Código base de ejemplo

```js
<script setup>
import { ref } from 'vue'

const acierto = ref('false')
const array = ref(['London', 'Berlin', 'Brussels', 'Paris'])
const contestada = ref(false)

const correctAnswer = ref('Paris')
const salidaClase = () => {
  return {
    error: contestada.value && !acierto.value,
    acierto: contestada.value && acierto.value,
    pendiente: !contestada.value,
  }
}
const shuffledArr = () => {
  contestada.value = false
  for (let i = array.value.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1))
    ;[array.value[i], array.value[j]] = [array.value[j], array.value[i]]
  }
}

const respuestaCorrecta = respuesta => {
  console.log(respuesta, respuesta === correctAnswer.value)
  acierto.value = (respuesta === correctAnswer.value)
  contestada.value = true
}
</script>

<template>
  <button type="button" @click="shuffledArr">Mezcla</button>
  <p v-text="salidaClase()"></p>
  <ul>
    <li
      v-for="respuesta in array"
      :key="respuesta"
      @click="respuestaCorrecta(respuesta)"
    >
      <div :class="salidaClase()">{{ respuesta }}</div>
    </li>
  </ul>
</template>

<style>
.error {
  color: red;
}
.acierto {
  color: aquamarine;
}
.pendiente {
  color: blue;
}
</style>
```
