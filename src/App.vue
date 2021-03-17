<template>
  <div class="app-container">
  	<header-section></header-section>
  	<main-section></main-section>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Main from './components/Main.vue';

export default {
  name: 'App',
  components: {
    'header-section': Header, 
    'main-section': Main
  }
}
</script>
