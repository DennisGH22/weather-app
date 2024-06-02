<template>
  <v-app>
    <v-main>
      <Navbar></Navbar>
	    <v-container>
        <v-row justify="center">
          <v-col cols="12" md="8">
            <v-text-field
              v-model="location"
              label="Enter Location"
              @keyup.enter="fetchWeather"
              outlined
              dense
            ></v-text-field>
            <v-btn @click="fetchWeather" color="primary">Get Weather</v-btn>
            <CurrentWeather :weather="currentWeather"></CurrentWeather>
            <WeatherForecast :forecast="forecast"></WeatherForecast>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <!-- <AppFooter /> -->
  </v-app>
</template>

<script>
  import axios from 'axios';
  import Navbar from './components/Navbar.vue';
  import CurrentWeather from './components/CurrentWeather.vue';
  import WeatherForecast from './components/WeatherForecast.vue';

  export default {
    name: 'App',
    components: {
      Navbar,
      CurrentWeather,
      WeatherForecast,
    },
    data() {
      return {
        location: '',
        currentWeather: null,
        forecast: null,
      };
    },
    methods: {
      async fetchWeather() {
        const apiKey = import.meta.env.VITE_API_KEY;
        const currentWeatherUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=${apiKey}&units=metric`;
        const forecastUrl = `https://api.openweathermap.org/data/2.5/forecast?q=${this.location}&appid=${apiKey}&units=metric`;

        try {
          const [currentWeatherResponse, forecastResponse] = await Promise.all([
            axios.get(currentWeatherUrl),
            axios.get(forecastUrl),
          ]);

          this.currentWeather = currentWeatherResponse.data;
          this.forecast = forecastResponse.data.list;
        } catch (error) {
          console.error(error);
        }
      },
    },
  };
</script>
