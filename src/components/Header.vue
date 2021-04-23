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
				<input 
					v-model="headerSearchInput" 
					v-on:input="headerSearchFunc"
					class="search-form__input" 
					type="text" 
					name="" 
					placeholder="Search">
				<button class="search-form__input-btn">
					<i class="fas fa-search"></i>
				</button>
			</form>
			<div 
				v-if="showSearchFailBanner" 
				class="search-fail-banner">
				<p class="search-fail-banner__text">Sorry, we can't find any results.</p>
				<button 
					v-on:click="clearHeaderSearch" 
					class="search-fail-banner__clear">
					<i class="fas fa-times"></i>
					Clear search
				</button>
			</div>
		</div>
	</div>
</template>

<script>
export default {
  	name: 'Header',
  	emits: ['clickedToggle'],
	data() {
		return {
			collapseSidebarData: false,
			headerSearchInput: '',
			showSearchFailBanner: false
		}
	},
	methods: {
		toggleSidebar: function () {
			// Toggle collapseSidebarData between true/false on click.
			this.collapseSidebarData = !this.collapseSidebarData;
			// Emit collapseSidebarData to be used in parent.
			this.$emit('clickedToggle', this.collapseSidebarData);
		},
		headerSearchFunc: function () {
			// Get nodeList of h2 elements with `card` class.
			const cardHeadingsAll = this.$parent.$el.querySelectorAll('.card h2:first-of-type');
			// Format search -> replace space (' ') with no space ('') and transform to lower case.
			const searchTerm = this.headerSearchInput.replace(/\s+/g, '').toLowerCase();
			// Remove any 'hide' classes to reset and recalculate.
			cardHeadingsAll.forEach(heading => {
				heading.closest('.card').classList.remove('header-search__hide-card');
			});
			// If there is a search term, filter through headings to find match.
			if (this.headerSearchInput.length > 0) {
				// Use spread to turn nodeList into array and filter it.
				const headerSearchFilter = [...cardHeadingsAll].filter(heading => {
					// Format heading text -> replace space (' ') with no space ('') and transform to lower case.
					const headingFormatted = heading.textContent.replace(/\s+/g, '').toLowerCase();
					// Return the headings that do NOT match -> a 'hide' class will be applied to their card.
					return !headingFormatted.includes(searchTerm);
				});
				headerSearchFilter.forEach(heading => {
					// Find closest parent of heading that has `.card` class and add class to hide it.
					heading.closest('.card').classList.add('header-search__hide-card');
				});
				// If filter returns the same amount of items as the number of total items, this means there
				// are no matches -> show fail banner.
				if (headerSearchFilter.length === cardHeadingsAll.length) {
					this.showSearchFailBanner = true;
				} else {
					this.showSearchFailBanner = false;
				}
			} else { // if there's no search term, remove all 'hide' classes.
				cardHeadingsAll.forEach(heading => {
					heading.closest('.card').classList.remove('header-search__hide-card');
				});
			}
		},
		clearHeaderSearch: function() {
			this.headerSearchInput = '';
			this.showSearchFailBanner = false;
			this.headerSearchFunc();
		}
	}
}
</script>

<style type="text/css">
	.header-main {
		align-items: center;
		background: #263955;
		display: flex;
		justify-content: flex-end;
		padding: .5rem .75rem;
		position: relative;
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

	.search-fail-banner {
		background: #f3dada;
		border-radius: .25rem;
	    bottom: -70px;
	    color: #580404;
	    display: flex;
	    align-items: center;
	    justify-content: space-between;
	    left: 1rem;
	    right: 1rem;
	    padding: .5rem 1rem;
	    position: absolute;
	}

	.search-fail-banner__clear {
		background: transparent;
		border: 0;
		color: #580404;
		font-size: 1rem;
		padding: .25rem .5rem;
		cursor: pointer;
	}

	.search-fail-banner__clear:hover {
		color: #9c0808;
	}

	.search-fail-banner__text {
		margin: 0;
	}

	.search-fail-banner__clear i {
		padding-right: .25rem;
	}

	@media screen and (min-width: 800px) {
		.header {
			display: grid;
			grid-template-columns: 250px 1fr;
		}

		.sidebar-collapse .header {
			grid-template-columns: 50px 1fr;
		}
		.sidebar-collapse .header-name {
			justify-content: center;
			padding: 0;
		}

		.sidebar-collapse .header-name__greeting {
			display: none;
		}
	}

</style>