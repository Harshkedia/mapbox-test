<template>
  <div>
    <div id="map" />
  </div>
</template>

<script>
import mapboxgl from "mapbox-gl";

export default {
  name: "HelloWorld",
  props: {},
  data() {
    return {
      map: null
    };
  },
  mounted() {
    this.createMap();
  },
  methods: {
    createMap() {
      mapboxgl.accessToken =
        "pk.eyJ1IjoiaGtlZGlhNzc5NyIsImEiOiJja2Mwc3FzODYxZjJmMnJsajdla3hhbm91In0.DuPVycamrmjI1eDuql2XqQ";
      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/streets-v11", // stylesheet location
        center: [-80, 50], // starting position [lng, lat]
        zoom: 9 // starting zoom
      });
    },
    addPoint(lat, long) {
      this.map.addSource("point", {
        type: "geojson",
        data: {
          type: "Feature",
          geometry: {
            type: "Point",
            coordinates: [lat, long]
          },
          properties: {
            "marker-symbol": "monument"
          }
        }
      });
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
