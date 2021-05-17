<template>
	<div class="maps">
        <Search
        placeholder="Search for a city"
        v-model:searchText="searchText"
        :search="searchLocation"
        />
      <MglMap
        :accessToken="accessToken"
        :mapStyle="mapStyle" />
    </div>
</template>

<script>
import Search from '../common/Search.vue';
import Mapbox from "mapbox-gl";
import { MglMap } from "vue-mapbox";

export default {
    name: 'Two',
    data: () => ({
        searchText: '',
        accessToken: import.meta.env.VITE_MAPS_API_KEY,
        mapStyle: 'mapbox://styles/mapbox/streets-v11',
    }),
    components: {
        Search,
        MglMap,
    },
    methods: {
        searchLocation() {
            console.log(this.searchText)
        },
    },
  created() {
    this.mapbox = Mapbox;
  }
}
</script>

<style>
.mgl-map-wrapper {
  height: 500px;
  width: 100%;
}
</style>
