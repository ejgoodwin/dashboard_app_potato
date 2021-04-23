<template>
	<div class="maps">
        <Search
        placeholder="Search for a city"
        v-model:searchText="searchText"
        :search="searchLocation"
        />
        <div id="map">
          <!-- <mapbox
          access-token="pk.eyJ1IjoicHVydml0cml2ZWRpIiwiYSI6ImNrYTU1Z3RnYzEwcHgza3AwYTU3c2h2ZDMifQ.3ZFchMC0MNZwHbY2Dz2MMA"
          :map-options="{
            style: 'mapbox://styles/mapbox/light-v9',
            center: [-96, 37.8],
            zoom: 3,
            }"
    /> -->
        </div>
    </div>
</template>

<script>
import Search from '../common/Search.vue';

export default {
    name: 'Two',
    data: () => ({
        searchText: '',
    }),
    components: {
        Search
    },
    methods: {
        searchLocation() {
            console.log(this.searchText)
        },
    },
}
</script>

<style>
.maps {
    border: 1px solid blue;
}

#map {
  width: 100%;
  height: 500px;
}
</style>
