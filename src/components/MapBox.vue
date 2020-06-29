<template>
  <div>
    <div id="map" />
  </div>
</template>

<script>
import mapboxgl from "mapbox-gl";

export default {
  name: "MapBox",
  props: {},
  data() {
    return {
      map: null
    };
  },
  mounted() {
    this.createMap();
    console.log(this.map.getBounds());
  },
  methods: {
    createMap() {
      mapboxgl.accessToken =
        "pk.eyJ1IjoiaGtlZGlhNzc5NyIsImEiOiJja2Mwc3FzODYxZjJmMnJsajdla3hhbm91In0.DuPVycamrmjI1eDuql2XqQ";
      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
        center: [-74.5, 40], // starting position [lng, lat]
        zoom: 9 // starting zoom
      });
      console.log(this.map);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#map {
  height: 500px;
  width: 500px;
}
</style>
