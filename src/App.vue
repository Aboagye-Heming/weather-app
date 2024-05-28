<template>
  <div class="app">
    <div class="header container h-100 p-5">
      <h1 class="mb-4">Weather App</h1>
      <div class="d-flex justify-content-center h-100">
        <div class="search-bar w-50 mx-2">
          <input
            v-model="city"
            type="text"
            class="input form-control"
            placeholder="Enter a city"
          />
        </div>
        <button class="btn-search btn btn-primary" @click="searchWeather">
          Search
        </button>
      </div>
      <div v-if="error" class="alert alert-danger mt-3">
        {{ error }}
      </div>
    </div>
    <Weather v-if="showWeather" :city="city" @error="handleError"></Weather>
  </div>
</template>

<script>
import Weather from "./components/WeatherReport.vue";

export default {
  name: "App",
  components: { Weather },
  data() {
    return {
      city: "",
      showWeather: false,
      error: null,
    };
  },
  methods: {
    async searchWeather() {
      this.error = null;
      this.showWeather = false;
      await this.$nextTick();
      this.showWeather = true;
    },
    handleError(errorMessage) {
      this.error = errorMessage;
      this.showWeather = false;
    },
  },
};
</script>

<style>
body {
  background-color: #121212 !important;
}
.header {
  background-color: #212730;
  border-radius: 20px;
  color: #fff;
  text-align: center;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  margin-top: 3rem;
}
.btn-search {
  background-image: linear-gradient(to left, cyan, magenta);
}
.alert {
  width: 50%;
  margin: 0 auto;
}
</style>
