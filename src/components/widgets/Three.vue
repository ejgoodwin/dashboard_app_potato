<template>
	<div class="cocktails">
		<h2>Discover a new cocktail</h2>
		<form v-on:submit.prevent="submitted">
			<label class="search-label" for="cocktail-search">Enter your favourite ingredient:</label>
			<input v-model="cocktailVal" type="text" id="cocktail-search">
			<input type="submit" value="search">
		</form>

		<div class="cocktail-results">
			<div class="cocktail-results__text">
				<ul class="cocktail-results__list">
					<li v-for="cocktail in cocktailRes">
						{{ cocktail.strDrink }}
					</li>
				</ul>
			</div>
			<div v-if="cocktailRes.length > 0" class="cocktail-results__image">
				<img :src="cocktailRes[0].strDrinkThumb">
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
			cocktailRes: []
		}
	},
	methods: {
		async submitted(event) {
			console.log();
			const response = await fetch(
			`https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=${this.cocktailVal}`)
			.then(res => res.json())
			.then(data => {
				this.cocktailRes = data.drinks.slice(1,6);
				console.log(this.cocktailRes[0]);
			});
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
		list-style: none;
		margin-top: 0;
		padding: 0;
	}

	.cocktail-results {
		display: flex;
		justify-content: space-between;
		padding-top: 1rem;
	}

	.cocktail-results__image {
		width: 30%;
	}

	.cocktail-results__image img {
		max-width: 100%;
	}

</style>