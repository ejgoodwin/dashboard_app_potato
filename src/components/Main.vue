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

<style type="text/css">
@media screen and (min-width: 800px) {
	.content {
		display: grid;
		grid-template-columns: 250px 1fr;
	}

	.sidebar-collapse .content {
		grid-template-columns: 50px 1fr;
	}
}
</style>