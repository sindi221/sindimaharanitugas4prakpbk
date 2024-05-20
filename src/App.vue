<template>
  <div id="app">
    <header>
      <h1>Weather Forecast</h1>
    </header>
    <main>
      <section class="location-section">
        <LocationSelector @locationSelected="handleLocationSelected" />
      </section>
      <section class="weather-section">
        <CurrentWeather :weather="currentWeather" />
        <WeatherForecast :weather="currentWeather" @locationSelected="updateWeather" />
      </section>
      <section class="animation-section">
        <WeatherAnimation :condition="currentWeather ? currentWeather.condition : ''" />
      </section>
      <section class="graph-section">
        <WeatherChart :forecastData="forecastData">
          <template #title>
            <span>Custom Weather Chart Title</span>
          </template>
          <template #day="{ day }">
            <div>
              <strong>{{ day.day }}</strong>
              <p>Temp: {{ day.temperature }}°C</p>
              <p>Weather: {{ day.condition }}</p>
            </div>
          </template>
        </WeatherChart>
      </section>
    </main>
  </div>
</template>

<script>
import LocationSelector from './components/LocationSelector.vue';
import CurrentWeather from './components/CurrentWeather.vue';
import WeatherForecast from './components/WeatherForecast.vue';
import WeatherAnimation from './components/WeatherAnimation.vue';
import WeatherChart from './components/WeatherChart.vue';

export default {
  name: 'App',
  components: {
    LocationSelector,
    CurrentWeather,
    WeatherForecast,
    WeatherAnimation,
    WeatherChart
  },
  data() {
    return {
      currentWeather: null,
      forecastData: []
    };
  },
  methods: {
    handleLocationSelected(location) {
      this.fetchWeatherData(location);
    },
    fetchWeatherData(location) {
      const weatherData = {
        city: location,
        temperature: Math.floor(Math.random() * (35 - 20 + 1)) + 20,
        condition: ['Sunny', 'Partly Cloudy', 'Cloudy', 'Rainy', 'Thunderstorms'][Math.floor(Math.random() * 5)]
      };
      this.updateWeather(weatherData);
    },
    updateWeather(weatherData) {
      this.currentWeather = weatherData;
      this.forecastData = this.generateForecastData();
    },
    generateForecastData() {
      const days = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'];
      const conditions = ['Sunny', 'Partly Cloudy', 'Cloudy', 'Rainy', 'Thunderstorms'];
      const forecastData = [];
      for (let i = 0; i < days.length; i++) {
        const temperature = Math.floor(Math.random() * (35 - 20 + 1)) + 20;
        const condition = conditions[Math.floor(Math.random() * conditions.length)];
        forecastData.push({ day: days[i], temperature, condition });
      }
      return forecastData;
    }
  }
}
</script>

<style scoped>
header {
  background-color: #db34a3;
  color: white;
  text-align: center;
  padding: 20px;
}

main {
  display: flex;
  justify-content: space-around;
  align-items: flex-start;
  flex-wrap: wrap;
  margin-top: 20px;
}

.location-section, .weather-section, .animation-section, .graph-section {
  width: 30%;
  margin-bottom: 20px;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h2 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.weather-condition {
  font-size: 1.2rem;
}

.button {
  display: inline-block;
  background-color: #c72ecc;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.button:hover {
  background-color: #8127ae;
}
</style>
