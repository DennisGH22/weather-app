<template>
<div v-if="forecast" class="weather-forecast">
  <v-container class="fill-height">
    <v-responsive
      class="align-centerfill-height mx-auto"
      max-width="900"
    >
	    <v-card class="mx-auto" max-width="600" outlined>
        <v-card-title>5-Day Forecast</v-card-title>
        <v-card-text>
          <v-row>
            <v-col
              v-for="(item, index) in filteredForecast"
              :key="index"
              cols="12"
              md="4"
            >
              <v-card outlined>
                <v-card-title>{{ formatDate(item.dt_txt) }}</v-card-title>
                <v-card-text>
                  <v-avatar size="64" class="mb-2">
                    <img :src="getIconUrl(item.weather[0].icon)" alt="Weather Icon">
                  </v-avatar>
                  <div>{{ item.weather[0].description }}</div>
                  <div>{{ item.main.temp }}°C</div>
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-responsive>
  </v-container>
</div>
</template>

<script>
  export default {
    name: 'WeatherForecast',
    props: {
      forecast: Array,
    },
    methods: {
      getIconUrl(icon) {
        return `https://openweathermap.org/img/wn/${icon}@2x.png`;
      },
      formatDate(date) {
        return new Date(date).toLocaleString('en-US', {
          weekday: 'short',
          hour: 'numeric',
          minute: 'numeric',
        });
      },
    },
    computed: {
      filteredForecast() {
        return this.forecast.filter((item, index) => index % 8 === 0);
      },
    },
  };
</script>

<style scoped>
  .weather-forecast {
    margin-top: 20px;
  }
</style>
