<template>
  <div class="days-tab text-center">
    <div v-if="loading" class="loading">Loading...</div>
    <ul v-else class="p-0">
      <li v-for="(day, index) in daysWeather" :key="index" class="li_active">
        <div class="py-3" style="height: 28rem"><img :src="day.iconUrl" alt="Weather icon" /></div>
        <div class="py-3">{{ day.date }}</div>
        <div class="py-3">{{ day.temperature }}&deg;C</div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";

export default {
  name: "DaysWeather",
  props: {
    cityName: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      loading: true,
      daysWeather: [],
    };
  },
  mounted() {
    this.fetchWeatherData();
  },
  methods: {
    async fetchWeatherData() {
      const apiKey = process.env.VUE_APP_WEATHER_API_KEY;
      const city = this.cityName;
      const apiUrl = `https://api.openweathermap.org/data/2.5/forecast?q=${city}&units=metric&appid=${apiKey}`;

      try {
        const response = await axios.get(apiUrl);
        const forecastData = response.data.list;

        const filteredData = forecastData
          .map((item) => {
            return {
              date: moment(item.dt_txt).format("dddd"),
              temperature: Math.round(item.main.temp),
              description: item.weather[0].description,
              iconUrl: `https://openweathermap.org/img/w/${item.weather[0].icon}.png`,
            };
          })
          .reduce((acc, item) => {
            if (!acc.some((day) => day.date === item.date)) {
              acc.push(item);
            }
            return acc;
          }, [])
          .slice(0, 4);

        this.daysWeather = filteredData;
        this.loading = false;
      } catch (error) {
        console.error("Error fetching weather data:", error);
        this.loading = false;
      }
    },
  },
};
</script>

<style>
.days-tab {
  width: 90%;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-radius: 20px;
  margin: auto;
  background-color: #343d4d;
}
.loading {
  color: #fff;
}
ul {
  margin: 0;
  padding: 0;
}
li {
  display: inline-block;
  list-style: none;
  height: 100%;
  width: 21%;
  max-width: 21%;
  font-size: 1vw;
  line-height: 1.2;
}
.li_active {
  background: #253d5c;
  color: #fff;
  border-radius: 0.5rem;
  margin: 0.5rem;
  font-weight: 600;
}
.li_active:hover {
  transform: scale(1.2);
  transition: transform 0.1s ease;
}
.li_active_temp {
  display: inline-block;
  background-color: #222831;
  color: #fff;
  transition: background-color 0.5s;
  border-radius: 10px;
}
</style>
