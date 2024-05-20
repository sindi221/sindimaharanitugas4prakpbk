<template>
  <div class="weather-forecast">
    <h2>Weather Forecast</h2>
    <p v-if="weather">City: {{ weather.city }}</p>
    <p v-if="weather">Temperature: {{ weather.temperature }}°C</p>
    <p v-if="weather">Condition: {{ weather.condition }}</p>
    <p v-else>Loading weather data...</p>
    <button @click="getLocation">Get Current Location Weather</button>
  </div>
</template>

<script>
export default {
  name: 'WeatherForecast',
  props: {
    weather: {
      type: Object,
      required: false,
      default: null
    }
  },
  methods: {
    getLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.fetchWeather);
      } else {
        alert('Geolocation is not supported by this browser.');
      }
    },
    fetchWeather(position) {
      const latitude = position.coords.latitude;
      const longitude = position.coords.longitude;
      console.log(`Latitude: ${latitude}, Longitude: ${longitude}`);
      const weatherData = {
        city: `Lat: ${latitude}, Lon: ${longitude}`,
        temperature: Math.floor(Math.random() * (35 - 20 + 1)) + 20,
        condition: ['Sunny', 'Partly Cloudy', 'Cloudy', 'Rainy', 'Thunderstorms'][Math.floor(Math.random() * 5)]
      };
      this.$emit('locationSelected', weatherData);
    }
  }
}
</script>

<style scoped>
.weather-forecast {
  padding: 30px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  text-align: left;
}

button {
  display: inline-block;
  background-color: #db347a;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #b92965;
}
</style>
