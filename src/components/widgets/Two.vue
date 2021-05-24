<template>
  <div class="maps">
    <Search
      placeholder="Search for a location"
      v-model:searchText="searchText"
      :search="searchLocation"
    />
    <div id="map" />
  </div>
</template>

<script>
import Search from "../common/Search.vue";
import mapboxgl from "mapbox-gl";
import "mapbox-gl/dist/mapbox-gl.css";

export default {
  name: "Two",
  data: () => ({
    searchText: "",
    map: '',
    accessToken: import.meta.env.VITE_MAPS_API_KEY,
    mapStyle: "mapbox://styles/mapbox/streets-v11",
    zoom: 14,
    center:[-0.0613707, 51.5348032],
    markers:[],
  }),
  components: {
    Search,
  },
  methods: {
    async searchLocation() {
      this.removeMarkers()

      const address = this.searchText.split(' ').join('+');
      const response = await fetch(`https://maps.googleapis.com/maps/api/geocode/json?address=${address}&key=${import.meta.env.VITE_GEOCODING_API_KEY}`);
      const result = await response.json();
      const center_lng = result.results[0].geometry.location.lng;
      const center_lat = result.results[0].geometry.location.lat;
      this.map.flyTo({center: [center_lng, center_lat], zoom:14});

      result.results.forEach(item => {
        const lng = item.geometry.location.lng;
        const lat = item.geometry.location.lat;
        const coord = [lng,lat];
        const el = document.createElement('div');
        el.className = 'marker';

        const marker = new mapboxgl.Marker(el).setLngLat(coord).addTo(this.map);
        this.markers.push(marker);
      })
    },
    removeMarkers() {
      this.markers.forEach(marker => {
        marker.remove();
      })

      this.markers = [];
    }
  },
  mounted() {
    mapboxgl.accessToken = import.meta.env.VITE_MAPS_API_KEY;
    this.map = new mapboxgl.Map({
      container: "map",
      style: this.mapStyle,
      center: this.center,
      zoom: 4
    });
    this.map.on("load", () => {
      const nav = new mapboxgl.NavigationControl();
      this.map.addControl(nav);
    });
  },
};
</script>

<style>
#map {
  border-radius: 8px;
  height: 500px;
  margin-top: 10px;
  width: 100%;
}

.marker {
  background-image: url('/src/assets/marker.svg');
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}
</style>
