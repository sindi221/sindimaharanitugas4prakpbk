<template>
  <div>
    <div v-if="weather">
      <h2>{{ weather.city }}</h2>
      <p>Temperature: {{ weather.temperature }}°C</p>
      <p>Condition: {{ weather.condition }}</p>
    </div>
    <div v-else>
      <p>Loading weather data...</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CurrentWeather',
  props: {
    weather: {
      type: Object,
      required: false,
      default: null
    }
  }
}
</script>

<style scoped>
h2 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

p {
  font-size: 1.2rem;
  margin: 5px 0;
}
</style>
