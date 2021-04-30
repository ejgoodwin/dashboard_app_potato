<template>
	<div class="header">
		<div class="header-name">
			<span class="header-name__greeting">Hi, Jane Doe</span>
			<button class="toggle" v-on:click="toggleSidebar()">
				<span class="toggle__line"></span>
				<span class="toggle__line"></span>
				<span class="toggle__line"></span>
			</button>
		</div>
		<div class="header-main">
			<form class="search-form">
				<input class="search-form__input" type="text" name="" placeholder="Search">
				<button class="search-form__input-btn">
					<i class="fas fa-search"></i>
				</button>
			</form>
		</div>
	</div>
</template>

<script>

export default {
  	name: 'Header',
  	emits: ['clickedToggle'],
	data() {
		return {
			collapseSidebarData: false
		}
	},
	methods: {
		toggleSidebar: function () {
			// Toggle collapseSidebarData between true/false on click.
			this.collapseSidebarData = !this.collapseSidebarData;
			// Emit collapseSidebarData to be used in parent.
			this.$emit('clickedToggle', this.collapseSidebarData);
		}
	}
}
</script>

<style type="text/css">
	.header {
		display: grid;
		grid-template-rows: 50px 50px;
	}

	.header-main {
		align-items: center;
		background: #263955;
		display: flex;
		justify-content: flex-end;
		padding: .5rem .75rem;
	}

	.search-form {
		display: flex;
		font-size: .875rem;
	}

	.search-form__input,
	.search-form__input-btn {
		padding: .5rem .75rem;
		border: none;
	}

	.search-form__input {
		border-top-left-radius: 1rem;
		border-bottom-left-radius: 1rem;
	}

	.search-form__input-btn {
		background: white;
		border-top-right-radius: 1rem;
		border-bottom-right-radius: 1rem;
		color: #A3A6B4;
	}

	.search-form__input::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
	  color: #989BA8;
	  opacity: 1; /* Firefox */
	}

	.search-form__input:-ms-input-placeholder { /* Internet Explorer 10-11 */
	  color: #989BA8;
	}

	.search-form__input::-ms-input-placeholder { /* Microsoft Edge */
	  color: #989BA8;
	}

	.header-name {
		align-items: center;
		background: rgb(0,155,214);
		background: linear-gradient(140deg, rgba(0,155,214,1) 0%, rgba(54,207,213,1) 100%);
		color: white;
		display: flex;
		font-weight: 700;
		justify-content: space-between;
		padding: .75rem;
	}

	.toggle {
		background: none;
		border: none;
	}

	.toggle:hover {
		cursor: pointer;
	}

	.toggle__line {
		background-color: white;
		border-radius: 5px;
		display: block;
		height: 2px;
		margin: 4px 0;
		width: 24px;
	}

	@media screen and (min-width: 800px) {
		.header {
			display: grid;
			grid-template-columns: 250px 1fr;
		}

		.sidebar-toggle .header {
			grid-template-columns: 50px 1fr;
		}
		.sidebar-toggle .header-name {
			justify-content: center;
			padding: 0;
		}

		.sidebar-toggle .header-name__greeting {
			display: none;
		}
	}

</style>