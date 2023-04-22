<script>
import WeatherTile from './WeatherTile.vue';
export default {
  props: ["data"],
  components: {WeatherTile},
}
</script>

<template>
  <div class="TilesContainer">
    <WeatherTile class="WeatherTile" :description="'Wind Speed'" :value="(this.data.wind.speed).toFixed(1)" :unit="'km/h'"><i class="bi bi-wind"></i></WeatherTile>
    <WeatherTile class="WeatherTile" :description="'Pressure'" :value="(this.data.main.pressure).toFixed(1)" :unit="'hPa'"><i class="bi bi-cloud-fog2"></i></WeatherTile>
    <WeatherTile class="WeatherTile" v-if="this.data.rain" :description="'Chance of rain'" :value="this.data.rain['1h']*100" :unit="'%'"><i class="bi bi-cloud-rain"></i></WeatherTile>
    <WeatherTile class="WeatherTile" v-if="!this.data.rain" :description="'Humidity'" :value="this.data.main.humidity" :unit="'%'"><i class="bi bi-water"></i></WeatherTile>
    <WeatherTile class="WeatherTile" :description="'Feels like'" :value="(this.data.main.feels_like-273.15).toFixed(1)" :unit="'°C'"><i class="bi bi-thermometer"></i></WeatherTile>
    </div>
</template>
