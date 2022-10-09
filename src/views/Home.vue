<template>
  <div class="weather">
    <h1 class="title">Weather App</h1>
    <form @submit.prevent="handleSubmit" class="input-city">
      <input type="text" v-model="cityName" placeholder="Enter name of city" />
      <p class="error">{{ error }}</p>
      <button>Show Result</button>
    </form>
    <WeatherInfo
      v-if="showWeatherbox"
      :cityName="cityTemp"
      :weatherRes="weathearResult"
    />
  </div>
</template>

<script>
import WeatherInfo from "../components/WeatherInfo.vue";
export default {
  components: { WeatherInfo },
  data() {
    return {
      showWeatherbox: false,
      cityName: "",
      cityTemp: "",
      error: "",
      apikey: "3045dd712ffe6e702e3245525ac7fa38",
      weathearResult: {},
    };
  },

  methods: {
    async handleSubmit() {
      this.weathearResult = await (
        await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.cityName}&appid=${this.apikey}`
        )
      ).json();
      if (this.weathearResult.cod == 404) {
        this.error = this.weathearResult.message;
        this.showWeatherbox = false;
      } else if (this.cityName == "") {
        this.error = "Enter city name";
        this.showWeatherbox = false;
      } else {
        this.showWeatherbox = true;
        this.cityTemp = this.cityName;
        this.cityName = "";
        this.error = "";
      }
    },
  },
};
</script>

<style>
.weather {
  position: relative;
  top: 13vh;
  width: 60%;
  background: #fff;
  border-radius: 24px;
  margin: 0 auto;
  padding: 20px;
}
.weather .title {
  color: #6c0404;
  border-bottom: solid 2px #6c0404;
  display: inline-block;
  padding-bottom: 8px;
}

.input-city {
  display: flex;
  flex-direction: column;
}

.input-city input {
  width: 80%;
  border: #cecdcd solid 1px;
  border-radius: 8px;
  padding: 8px;
  margin: 0 auto;
  font-size: 16px;
}
.input-city button {
  width: 150px;
  height: 45px;
  border-radius: 10px;
  border: 0;
  cursor: pointer;
  margin: 0 auto;
  background: #6c0404;
  color: #fff;
  font-size: 16px;
}

.input-city button:hover {
  background: #ae0808;
}
.error {
  font-size: 20px;
  color: red;
  font-weight: 700;
  margin-bottom: 24px;
}
</style>