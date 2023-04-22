<script>
export default {
  data() {
    return {
      data: {},
      cityInput: ""
    }
  },
  methods: {
    onCityInput () {
         this.$emit('CityInput', this.cityInput)
         this.cityInput = ""
     }
  }
}
</script>

<template>
  <div class="navbar">
    <div class="navDateContainer">
        <h3 id="navMonth">{{ new Date(Date.now()).toLocaleDateString("en-US", {year: "numeric", month: "long"}) }}</h3>
        <p id="navDate">{{ new Date(Date.now()).toLocaleDateString("en-US", {weekday: "long", month: "short", day: "numeric"}) }}</p>
    </div>
    <span class="textbox"> 
        <i class="bi bi-search" id="searchIcon"></i>
        <form v-on:submit.prevent="onCityInput">
          <input type="text" id="citySearch" name="citySearch" placeholder="Search city here" v-model="this.cityInput"/>
          <button type="submit" style="display: none"></button>
        </form>
    </span>
  </div>
</template>
