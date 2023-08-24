<template>
  <component :is="currentView"></component>
</template>

<script setup>
import { ref, computed } from 'vue';
import WorldsPage from './WorldsPage.vue';
import CharacterOverviewPage from './CharacterOverviewPage.vue';

const routes = {
  '/': WorldsPage,
  '/worldName': CharacterOverviewPage
}

const currentPath = ref(window.location.pathname);

window.addEventListener('hashchange', () => {
  currentPath.value = window.location.pathname;
});

const currentView = computed(() => {
  // return routes['/']
  if (currentPath.value.split('/') == 3) {
    return 0;
  }
  else if (currentPath.value.split('/')[1] != "") {
    return routes['/worldName'];
  }
  else {
    return routes['/'] //|| NotFound
  }
});
</script>

<script>
console.log((window.location.pathname).split('/'));
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
