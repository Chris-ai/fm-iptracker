<template>
  <l-map style="z-index: 0" :zoom="zoom" :center="center">
    <l-tile-layer :url="url"></l-tile-layer>
    <l-marker :icon="icon" :lat-lng="markerLatLng"></l-marker>
  </l-map>
</template>

<script>
import { LMap, LTileLayer, LMarker } from "vue2-leaflet";
import { icon } from "leaflet";

export default {
  components: {
    LMap,
    LTileLayer,
    LMarker,
  },
  props: ["LatLng"],
  data() {
    return {
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      // attribution:
      //   '&copy; <a target="_blank" href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      zoom: 15,
      center: this.LatLng,
      markerLatLng: this.LatLng,
      icon: icon({
        iconUrl: "icon-location.svg",
        iconSize: [32, 37],
        iconAnchor: [16, 37],
      }),
    };
  },
  mounted() {},
};
</script>

<style lang="scss"></style>