<template>
<div v-if="weather" class="current-weather">
  <v-card class="mx-auto" max-width="400" outlined>
    <v-card-title>{{ weather.name }}</v-card-title>
    <v-card-text>
      <v-row>
        <v-col cols="12">
          <v-avatar size="64" class="mb-2">
            <img :src="weatherIconUrl" alt="Weather Icon">
          </v-avatar>
        </v-col>
        <v-col cols="12">
          <div>{{ weather.weather[0].description }}</div>
          <div>{{ weather.main.temp }}°C</div>
          <div>Humidity: {{ weather.main.humidity }}%</div>
          <div>Wind: {{ weather.wind.speed }} m/s</div>
        </v-col>
      </v-row>
    </v-card-text>
  </v-card>
</div>
</template>

<script>
  export default {
    name: 'CurrentWeather',
    props: {
      weather: Object,
    },
    computed: {
      weatherIconUrl() {
        return `https://openweathermap.org/img/wn/${this.weather.weather[0].icon}@2x.png`;
      },
    },
  };
</script>

<style scoped>
  .current-weather {
    margin-top: 20px;
  }
</style>
