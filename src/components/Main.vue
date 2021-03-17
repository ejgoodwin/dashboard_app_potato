<template>
  <div class="content">
    <sidebar></sidebar>
    <dashboard></dashboard>
  </div>
</template>

<script>
import Sidebar from './Sidebar.vue';
import Dashboard from './Dashboard.vue';
export default {
  name: 'Main',
  components: {
  	'sidebar': Sidebar,
  	'dashboard': Dashboard
  }
}
</script>