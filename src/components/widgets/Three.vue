<template>
	<div class="card cocktails">
		<h2>Discover a new cocktail</h2>
		<form v-on:submit.prevent="submitted" class="card-search">
			<label class="search-label" for="cocktail-search">
				Enter your favourite ingredient:
			</label>
			<div class="card-search__input-container">
				<input 
					v-model="cocktailVal" 
					type="text" 
					id="cocktail-search"
					class="card-search__input"
					placeholder="Gin, whiskey, rum...">
				<button class="card-search__input-btn">
					<i class="fas fa-search"></i>
				</button>
				<button 
					class="card-search__input-btn-clear"
					:class="cocktailVal.length > 0 ? 'card-search__input-btn-clear--show' : null"
					v-on:click.prevent="clearSearch">
					<i class="fas fa-times"></i>
				</button>
			</div>
		</form>

		<div 
			class="card-error"
			:class="cocktailError ? 'card-error--show' : null">
			Sorry, I don't recognise that ingredient.
		</div>

		<div 
			class="cocktail-results"
			:class="cocktailRes.length === 0 ? 'cocktail-results--no-results' : null">
			<div class="cocktail-results__text">
				<ul class="cocktail-results__list">
					<li 
						v-for="(cocktail, index) in cocktailRes"  
						v-bind:class="this.selectedDrink === index ? 'cocktail-results__item--active' : null"
						class="cocktail-results__item">
						<button 
							v-on:click="displayDrink(index)"
							class="cocktail-results__list-button">
							{{ cocktail.strDrink }}
						</button>
					</li>
				</ul>
			</div>
			<div v-if="cocktailRes.length > 0" class="cocktail-results__image-container">
				<img :src="drinkImage" class="cocktail-results__image">
			</div>
		</div>
	</div>
</template>

<script>

export default {
	name: 'Three',
	data () {
		return {
			cocktailVal: '',
			cocktailRes: [],
			drinkImage: '',
			selectedDrink: 0,
			clearSearchVisible: false,
			cocktailError: false
		}
	},
	methods: {
		async submitted(event) {
			const response = await fetch(
			`https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=${this.cocktailVal}`)
			.then(res => res.json())
			.then(data => {
				// Assign the drinks data to cocktailRes.
				this.cocktailRes = data.drinks;
				// Set the drink image as the first item's image.
				this.drinkImage = data.drinks[0].strDrinkThumb;
				// Set the selected drink to the first item.
				this.selectedDrink = 0;
				// Make sure error state is false.
				this.cocktailError = false;
			})
			.catch(error => {
				console.log("error" + error);
				// Reset cocktail array if nothing is returned.
				this.cocktailRes = [];
				// Change error state to true.
				this.cocktailError = true;
				
			});
			// Reset input value.
			this.cocktailVal = '';
		},
		displayDrink(index) {
			// Change `selectedDrink` to clicked button to ensure active styling.
			this.selectedDrink = index;
			// Change the drink image to selected.
			this.drinkImage = this.cocktailRes[index].strDrinkThumb;
		},
		clearSearch() {
			// Reset the input value.
			this.cocktailVal = '';
		}
	}
}
</script>

<style type="text/css">
	.search-label {
		display: block;
		padding-bottom: .5rem;
	}

	.cocktail-results__list {
		height: 200px;
		list-style: none;
		margin: 0;
		overflow: scroll;
		padding: 0;
		border: 1px solid #A3A6B4;
		border-radius: .25rem;
	}

	.cocktail-results__list-button {
		background: white;
		border: 0;
		border-bottom: 1px solid #A3A6B4;
		cursor: pointer;
		padding: .375rem .5rem;
		position: relative;
		text-align: left;
		width: 100%;
	}

	.cocktail-results__list-button:hover {
		background: #f7fafb;
	}

	.cocktail-results__item:first-of-type .cocktail-results__list-button {
		border-top-left-radius: .25rem;
		border-top-right-radius: .25rem;
	}

	.cocktail-results__item:last-of-type .cocktail-results__list-button {
		/* Ensure last item is clickable - move above gradient pseudo el. */
		margin-bottom: 20px;
	}

	.cocktail-results__item--active .cocktail-results__list-button {
		background: #eef7fb;
		border-color: #00adef;
		padding-left: 1rem;
		transition: .2s;
	}

	.cocktail-results__item .cocktail-results__list-button::before {
		color: #00adef;
		content: '\f0da';
		font-family: "Font Awesome 5 Free"; 
		font-weight: 900;
		position: absolute;
		left: -20px;
		font-size: 1rem;
		transition: .2s;
	}


	.cocktail-results__item--active .cocktail-results__list-button::before {
		left: 5px;

	}

	.cocktail-results {
		display: flex;
		justify-content: space-between;
		padding: 1rem 0 0;
	}

	.cocktail-results--no-results {
		display: none;
	}

	.cocktail-results__text {
		flex-grow: 1;
		margin: 0 1rem 0 0;
		position: relative;
	}

	.cocktail-results__text::after {
		background: rgb(255,255,255);
		background: linear-gradient(0deg, rgba(255,255,255,1) 0%, rgba(255,255,255,0) 100%);
		border-bottom-left-radius: .26rem;
		border-bottom-right-radius: .26rem;
		bottom: 1px;
		content: '';
		height: 20px;
		left: 1px;
		position: absolute;
		right: 1px;
	}

	.cocktail-results__image-container {
		width: 30%;
	}

	.cocktail-results__image {
		border-radius: .25rem;
		max-width: 100%;
	}

</style>