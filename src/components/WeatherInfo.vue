<template>
  <div class="weather-info">
    <div>
      <img
        class="weather-img"
        src="../assets/clear.jpg"
        v-if="isClear"
      />
      <img
        class="weather-img"
        src="../assets/cloud.jpg"
        v-if="isCloud"
      />
      <img
        class="weather-img"
        src="../assets/mist.jpg"
        v-if="isMist"
      />
      <img
        class="weather-img"
        src="../assets/snow.jpg"
        v-if="isSnow"
      />
      <img
        class="weather-img"
        src="../assets/rain.jpg"
        v-if="isRain"
      />
    </div>
    <div>
      <h1 class="city">{{ weatherRes.name }}</h1>
      <h2 class="temp">{{ temp }} C</h2>
      <h2 class="wind">Wind Speed: {{ weatherRes.wind.speed }} km/h</h2>
      <img class="icon" :src="iconSrc" />
      <h2 class="des">{{ weatherRes.weather[0].description }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  props: ["cityName", "weatherRes"],
  data() {
    return {
      temp: (this.weatherRes.main.temp - 273.15).toFixed(2),
      iconSrc:
        "http://openweathermap.org/img/wn/" +
        this.weatherRes.weather[0].icon +
        "@2x.png",
      isClear: false,
      isCloud: false,
      isMist: false,
      isSnow: false,
      isRain: false,
    };
  },
  mounted() {
    this.isClear =
      this.weatherRes.weather[0].description == "clear sky" ? true : false;
    this.isCloud =
      this.weatherRes.weather[0].description == "few clouds" ||
      this.weatherRes.weather[0].description == "scattered clouds" ||
      this.weatherRes.weather[0].description == "broken clouds"
        ? true
        : false;
    this.isRain =
      this.weatherRes.weather[0].description == "shower rain" ||
      this.weatherRes.weather[0].description == "rain" ||
      this.weatherRes.weather[0].description == "thunderstorm"
        ? true
        : false;
    this.isSnow =
      this.weatherRes.weather[0].description == "snow" ? true : false;
    this.isMist =
      this.weatherRes.weather[0].description == "mist" ? true : false;
  },
  updated() {
    this.isClear =
      this.weatherRes.weather[0].description == "clear sky" ? true : false;
    this.isCloud =
      this.weatherRes.weather[0].description == "few clouds" ||
      this.weatherRes.weather[0].description == "scattered clouds" ||
      this.weatherRes.weather[0].description == "broken clouds"
        ? true
        : false;
    this.isRain =
      this.weatherRes.weather[0].description == "shower rain" ||
      this.weatherRes.weather[0].description == "rain" ||
      this.weatherRes.weather[0].description == "thunderstorm"
        ? true
        : false;
    this.isSnow =
      this.weatherRes.weather[0].description == "snow" ? true : false;
    this.isMist =
      this.weatherRes.weather[0].description == "mist" ? true : false;
  },
};
</script>

<style>
.weather-info {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  margin-top: 30px;
  width: 80%;
  margin: 0 auto;
}

.des {
  margin: 0;
  text-align: center;
}

.wind {
  margin: 0;
}
.temp {
  font-size: 50px;
  margin: 10px 0;
}
.city {
  font-size: 50px;
  margin: 10px 0;
}
.icon {
  margin: 0 auto;
}
.weather-img {
  border-radius: 20px;
  width: 100%;
  height: 250px;
}

@media(max-width: 1325px){
  .weather-info{
    justify-content: center;
    margin-top: 16px;
  }
  .weather-img{
    height: auto;
  }
}
</style>