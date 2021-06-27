<template>
	  <div class="dashboard">
	  	<one class="card"></one>
	  	<two class="card"></two>
	  	<three class="card"></three>
	  	<four class="card"></four>
	  </div>
</template>

<script>
import One from './widgets/One.vue';
import Two from './widgets/Two.vue';
import Three from './widgets/Three.vue';
import Four from './widgets/Four.vue';

export default {
  name: 'Dashboard',
  components: {
  	'one': One,
  	'two': Two,
  	'three': Three,
  	'four': Four
  }
}
</script>


<style type="text/css">
	.dashboard {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 16px;
		padding: 16px;
	}

	@media screen and (max-width: 550px) {
		.dashboard {
			grid-template-columns: 1fr;
		}
	}
</style>