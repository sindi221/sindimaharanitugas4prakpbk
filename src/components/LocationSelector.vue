<template>
  <div class="location-selector">
    <select v-model="selectedLocation" @change="emitLocation">
      <option disabled value="">Select a location</option>
      <option value="New York">New York</option>
      <option value="Tokyo">Tokyo</option>
      <option value="London">London</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'LocationSelector',
  data() {
    return {
      selectedLocation: ''
    };
  },
  methods: {
    emitLocation() {
      this.$emit('locationSelected', this.selectedLocation);
    }
  }
}
</script>

<style scoped>
.location-selector {
  margin: 20px 0;
}

select {
  padding: 10px;
  font-size: 1rem;
  border-radius: 5px;
  border: 1px solid #ccc;
}
</style>
