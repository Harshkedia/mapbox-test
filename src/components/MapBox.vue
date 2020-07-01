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
    console.log(process.env.MAPBOX_API_KEY);
    this.createMap();
    this.map.on("load", () => {
      this.addPoint(-74.5, 40);
      console.log(this.map);
    });
    console.log(this.map.getBounds());
  },
  methods: {
    createMap() {
      mapboxgl.accessToken = process.env.MAPBOX_API_KEY;
      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/mapbox/light-v10", // stylesheet location
        center: [-74.5, 40], // starting position [lng, lat]
        zoom: 9 // starting zoom
      });
    },
    addPoint(long, lat) {
      this.map.addSource("my-data", {
        type: "geojson",
        data: {
          type: "Feature",
          geometry: {
            type: "Point",
            coordinates: [long, lat]
          },
          properties: {
            name: "Dinagat Islands",
            "marker-symbol": "monument"
          }
        }
      });

      this.map.addLayer({
        id: "my-data",
        type: "symbol",
        source: "my-data",
        layout: {
          "icon-image": "volcano-15",
          "icon-size": 1.5
        }
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#map {
  width: 80%;
  height: 800px;
  margin: 0 auto;
}
</style>
