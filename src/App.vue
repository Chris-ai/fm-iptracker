<template>
  <div id="app">
    <header>
      <IpTracker @latLng="handleLatLangChange" />
    </header>
    <section>
      <Map :key="key" v-bind:LatLng="markerLatLng" />
    </section>
  </div>
</template>

<script>
import Map from "@/components/Map.vue";
import IpTracker from "@/components/IpTracker.vue";

export default {
  name: "App",
  components: {
    Map,
    IpTracker,
  },
  data() {
    return {
      markerLatLng: [],
      key: 0
    };
  },
  methods: {
    handleLatLangChange(tab) {
      console.log("tab", tab);
      this.markerLatLng = tab;
      this.key += 1
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Rubik:wght@400;500;700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;

  --very-dark-gray: hsl(0, 0, 17%);
  --dark-gray: hsl(0, 0%, 59%);

  --fw-regular: 400;
  --fw-medium: 500;
  --fw-bold: 700;
  font-family: "Rubik", sans-serif;
}

#app {
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;

  header {
    flex: 0 1 auto;
  }

  section {
    flex: 1 1 auto;
  }
}
</style>