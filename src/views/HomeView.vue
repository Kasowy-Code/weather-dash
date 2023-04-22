<script>
import GeneralInfo from "../components/GeneralInfo.vue";
import TilesContainer from "../components/TilesContainer.vue";
import Navbar from "../components/Navbar.vue";
import WeeklyForecast from "../components/WeeklyForecast.vue";
import Percipitation from "../components/Percipitation.vue";
import SunTimes from "../components/SunTimes.vue";
import axios from "axios";
export default {
  components: { GeneralInfo, TilesContainer, Navbar, WeeklyForecast, Percipitation, SunTimes },
  data() {
    return {
      currentData: {},
      forecastData: {},
      city: "Szczecin",
      prevCity: "Szczecin",
      icon: "",
      loaded: false,
      error: false,
    }
  },mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios.get("https://api.openweathermap.org/data/2.5/weather?q="+this.city+"&appid="+import.meta.env.VITE_API_KEY)
    .then((res)=>{
      console.log(res.data);
      this.currentData = res.data;
      console.log(this.currentData);
      axios.get("https://api.openweathermap.org/data/2.5/forecast?lat="+this.currentData.coord.lat+"&lon="+this.currentData.coord.lon+"&appid="+import.meta.env.VITE_API_KEY)
      .then(forecast => {
        this.forecastData = forecast.data;
        // console.log(this.forecastData.list.slice(0, 5));
        this.loaded = true;
      })
    }).catch(()=>{

      this.error = true;
      this.city = this.prevCity;
      setTimeout(()=>this.error=false, 5000);
    }
    )
    },
    onCityInput(v) {
      this.prevCity = this.city;
      this.city = v;
      this.fetchData();
    }
  }
}
</script>

<template>
  <main v-if="this.loaded">
    <div class="main">
      <div v-if="this.error" class="Toast">Something went wrong!</div>
      <div class="left">
        <Navbar @CityInput="onCityInput" />
        <h3>Today overview</h3>
        <TilesContainer :data="this.currentData"></TilesContainer>
        <h3>Weather Forecast</h3>
        <WeeklyForecast :data="this.forecastData"></WeeklyForecast>
      </div>
      <div class="right">
        <GeneralInfo :city="this.city" :temperature="(this.currentData.main.temp-273.15).toFixed(1)" :description="this.currentData.weather[0].description" :icon="'https://openweathermap.org/img/wn/'+this.currentData.weather[0].icon+'.png'" :timezone="this.currentData.timezone"></GeneralInfo>
        <h3 class="rightText">Precipitation</h3>
        <Percipitation :data="this.forecastData.list.slice(0,4)"></Percipitation>
        <h3 class="rightText">Sunrise & Sunset</h3>
        <SunTimes :data="this.currentData"></SunTimes>
      </div>
    </div>
  </main>
  
</template>
