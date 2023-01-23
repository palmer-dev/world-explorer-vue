<template>
  <div class="container">
    <div>
      <label for="selectMapType">Choisissez un type de carte : &nbsp;</label>
      <select v-model="selectedMapType" name="selectMapType" id="selectMapType">
        <option value="">Carte routière</option>
        <option value="k">Satellite</option>
      </select>
    </div>
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

.container {
  background-color: white;
  border-radius: 10px;
  padding: 10px;
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  gap: 10px;
}
</style>