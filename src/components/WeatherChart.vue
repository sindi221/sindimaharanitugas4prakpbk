<template>
  <div class="weather-chart">
    <h2><slot name="title">Weather Graph</slot></h2>
    <ul v-if="forecastData.length">
      <li v-for="day in forecastData" :key="day.day" class="weather-day">
        <slot name="day" :day="day">
          <p>{{ day.day }}</p>
          <p>Temperature: {{ day.temperature }}°C</p>
          <p>Condition: {{ day.condition }}</p>
        </slot>
      </li>
    </ul>
    <p v-else>No forecast data available.</p>
  </div>
</template>

<script>
export default {
  name: 'WeatherChart',
  props: {
    forecastData: {
      type: Array,
      required: true,
      default: () => []
    }
  }
}
</script>

<style scoped>
.weather-chart {
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  text-align: left;
}

ul {
  list-style-type: none;
  padding: 0;
}

.weather-day {
  margin-bottom: 15px;
}

.weather-day p {
  margin: 5px 0;
}
</style>
