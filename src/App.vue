<template>
  <div id="app">
    <div class="container mx-auto">
    <div class="flex flex-wrap justify-start mx-10">
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
    </div>
  </div>
  </div>
</template>

<script>
import BreadCrumbsDl from '@/components/BreadCrumbsDl.vue';

function handler(route) {
  console.log(route);
}

function data() {
  return {
    routes: [
      { path: '/', meta: { title: 'Principal' } },
      { path: '/products', meta: { title: 'Productos' } },
      { path: '/categories', meta: { title: 'Categoría' } },
      { path: '/profile', meta: { title: 'Perfil' } },
    ],
  };
}

export default {
  name: 'App',
  components: {
    bcDl: BreadCrumbsDl,
  },
  data,
  methods: {
    handler,
  },
};
</script>

<style lang="scss">
@import './src/assets/styles.scss';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

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
</style>
