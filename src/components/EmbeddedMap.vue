<template>
  <div>
    <select v-model="selectedMapType">
      <option value="">Carte routière</option>
      <option value="k">Satellite</option>
    </select>
    <iframe :src="mapSrc" frameborder="0" scrolling="no" marginheight="0" marginwidth="0"
      class="map-container"></iframe>
  </div>
</template>
<script>
export default {
  name: "EmbeddedMap",
  props: {
    query: {
      type: String,
      default: "Place Bellecour, Lyon, France",
    },
    zoom: {
      type: Number,
      default: 2,
    },
    mapType: {
      type: String,
      default: ""
    }
  },
  computed: {
    mapSrc: function () {
      return `https://maps.google.com/maps?q=${this.query}&t=${this.selectedMapType}&z=${this.zoom}&ie=UTF8&iwloc=&output=embed`;
    },
  },
  data() {
    return {
      selectedMapType: ""
    }
  },
  mounted() {
    this.selectedMapType = this.mapType;
  },
  watch: {
    mapType: function (newType) {
      this.selectedMapType = newType;
    },
    selectedMapType: function (newType) {
      this.$emit("mapTypeChange", newType);
    }
  }
};
</script>
<style scoped>
.map-container {
  width: 100%;
  height: 500px;
}
</style>