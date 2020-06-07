# bread-crumbs-dl
Bread crumbs en [vivo](https://codepen.io/JOSEJUAN/pen/OJMVYJW)

Este es un componente para ser usado como **bread-crumbs** en las aplicaciones sin embargo el también se presta para usarse en la representación de flujos unidireccionales o en líneas de tiempo.

## Install
```js
npm i bread-crumbs-dl
```

## Use
Uso global en la aplicación con el nombre `bread-crumbs-dl`:

`main.js`
```js
import { install } from 'bread-crumbs-dl';

Vue.use(install);
...
...
new Vue({
    el: '...'
})
```
o si quieres cambiarle el nombre al componente:
```js
import breadCrumbsDl from 'bread-crumbs-dl';

Vue.component('my-component-name', breadCrumbsDl)
...
...
new Vue({
    el: '...'
})
```
Luego, en cualquier archivo `.vue` puede ser usado.
```html
<template>
    <bread-crumbs-dl />
</template>
```
Si prefieres importar el archivo directamente en el archivo en el que lo usarás, por ejemplor en `cualquierArchivo.vue`:
```html
<template>
    <bread-crumbs-dl />
</template>
```
```js
import BreadCrumbsDl from 'bread-crumbs-dl';

export default {
    components: {
        breadCrumbsDl: BreadCrumbsDl,
    }
}
```
## Cómo usarlo
El componente tiene las siguientes propiedades:
Nombre|Tipo|Valores|Descripción|
:-----|:---|:------|:----------|
`text`|String| cualquiera|Es el contenido mostrado en el componente. Por defecto: `''`
`color`|String|`#f9f9f9`|Corresponde al color de fondo del componente. Por defecto `currentColor`.
`color-text`|String|`#000000`|Corresponde al color del texto en el componente. Por defecto `white`.

Es importante definir ciertos estilos para el componente como: ancho automático y el alto definido. La primera propiedad es necesaria para que el componente se ajuste de acuerdo al texto a mostrar. La tercera propiedad importante es el `margin-right` para que separe los componentes.
Es posible asignar los colores por estilos y no directamente en las propiedades:
```html
<bc-dl
    v-for="(route, index) in routes"
    :key="index"
    :class="[
    'bc-dl-container',
    { 'selected': index === routes.length - 1 }
    ]"
    :text="route.meta.title"
    @click="handler(route)"
/>
```
```css
.bc-dl-container.bc-container {
    @apply w-auto h-20 mr-2 my-1;
    @apply cursor-pointer;
    .bc-svg {
      fill: rgb(76, 128, 224);
      .bc-text {
        @apply text-2xl font-bold;
      }
    }
  }
  .selected.bc-container {
    .bc-svg {
      fill: rgb(50, 231, 50);
    }
  }
```
> `bc.container`: es la clase principal del componente usada para acceder a las clases de los elementos internos.

> `.bc-svg`: es la clase del elemento `svg` y se usa para asignar el valor a `fill`

> `.bc-text`: es la clase del elemento `<text>` encargado de renderizar el texto.

Adicionalmente se puede escuchar el evento `@click` en el componente
```html
<template>
    <bread-crumbs-dl @click="clickHandler"/>
</template>
```