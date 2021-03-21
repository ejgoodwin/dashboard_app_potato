<template>
  <div class="app-container" v-bind:class="collapseSidebar ? 'sidebar-collapse': 'sidebar-expand'">
  	<header-section @clicked="toggleSidebar"></header-section>
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
  },
  data() {
  	return {
  		collapseSidebar: false
  	}
  },
  methods: {
  	// When toggle btn in header is clicked, assign emitted data to collapseSidebar.
  	// Use to apply class to app-container to show if sidebar is collapsed or expanded.
    toggleSidebar (toggleData) {
    	this.collapseSidebar = toggleData;
    }
  }
}
</script>
