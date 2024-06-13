<template>
  <div class="container p-0">
    <div class="d-flex mt-4">
      <div class="card main-div w-100">
        <div class="p-3">
          <h2 class="mb-1 day">Today</h2>
          <h2 class="place">
            <i class="fa fa-location"
              >{{ name }} <small>{{ country }}</small></i
            >
          </h2>
          <div class="temp">
            <h1 class="weather-temp">{{ temperature }}&deg;C</h1>
            <h2 class="text-light">{{ description }} <img :src="iconUrl" /></h2>
          </div>
        </div>
      </div>
      <div class="card card-2 w-100">
        <table class="m-4">
          <tbody>
            <tr>
              <th>Humidity</th>
              <td>{{ humidity }}%</td>
            </tr>
            <tr>
              <th>Wind</th>
              <td>{{ wind }} m/s</td>
            </tr>
            <tr>
              <th>Pressure</th>
              <td>{{ pressure }} hPa</td>
            </tr>
          </tbody>
        </table>
        <DaysWeather :cityName="cityName"></DaysWeather>
        <div id="div_Form" class="d-flex m-3 justify-content-center">
          <button @click="changeLocation" class="btn change-btn btn-primary">
            Change Location
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import DaysWeather from "./DaysWeather.vue";

export default {
  name: "WeatherReport",
  components: { DaysWeather },
  props: {
    city: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      cityName: this.city,
      temperature: null,
      description: null,
      iconUrl: null,
      humidity: null,
      pressure: null,
      wind: null,
      country: null,
      name: null,
    };
  },
  methods: {
    async fetchWeather() {
      const apiKey = process.env.VUE_APP_WEATHER_API_KEY;
      const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${apiKey}`;

      try {
        const response = await axios.get(apiUrl);
        const weatherData = response.data;
        this.temperature = Math.round(weatherData.main.temp);
        this.description = weatherData.weather[0].description;
        this.iconUrl = `https://openweathermap.org/img/w/${weatherData.weather[0].icon}.png`;
        this.humidity = weatherData.main.humidity;
        this.pressure = weatherData.main.pressure;
        this.wind = weatherData.wind.speed;
        this.country = weatherData.sys.country;
        this.name = weatherData.name;
      } catch (error) {
        this.$emit("error", "City not found. Please enter a valid city.");
        console.error("Error fetching weather data:", error);
      }
    },
    changeLocation() {
      window.location.reload();
    },
  },
  created() {
    this.fetchWeather();
  },
};
</script>

<style>
body {
  border-color: #343d4d;
}
.weather-temp {
  margin: 0;
  font-weight: 700;
  font-size: 4em;
  color: #fff;
}
h2.mb-1.day {
  font-size: 3rem;
  font-weight: 400;
  color: #fff;
}
.place {
  color: #fff;
}
.main-div {
  border-radius: 20px;
  color: #fff;
  background-image: url("../assets/images/ghana-beach.webp");
  background-size: cover;
  background-position: center;
  background-color: rgba(0, 0, 0, 0.5);
  background-repeat: no-repeat;
  height: 28rem;
}
.temp {
  position: absolute;
  bottom: 0;
}
.main-div:hover {
  transform: scale(1.1);
  transition: transform 0.5s ease;
  z-index: 1;
}
.card-2 {
  background-color: #212730 !important;
  border-radius: 20px;
}
table {
  border-collapse: separate;
  border-spacing: 15px;
  width: 85%;
  text-align: left;
  max-width: 600px;
  margin: 0 auto;
}
th,
td {
  font-size: 18px;
  color: #fff;
}
td {
  text-align: right;
}
.change-btn {
  background-image: linear-gradient(to right, cyan, magenta);
}
.change-btn:hover {
  transform: scale(0.9);
}
</style>
