<script>
  export default {
    
    data() {
      return {
        clock: ""
      }
    },
    created() {
      let date = new Date(Date.now()+(new Date().getTimezoneOffset()*60 + this.timezone)*1000);
      this.clock = date.toString().substring(16, 21)
      setInterval(()=>{
        let date = new Date(Date.now()+(new Date().getTimezoneOffset()*60 + this.timezone)*1000);
      this.clock = date.toString().substring(16, 21)
      }, 1000)
    },
    methods: {
      onCityInput (event) {
           this.$emit('CityInput', this.cityInput)
       }
    },
    props: {
      description: {
        type: String,
        required: true
      },
      temperature: {
        type: String,
        required: true
      },
      icon: {
        type: String,
        required: true
      },
      city: {
        type: String,
        required: true
      },
      timezone: {
        type: Number,
        required: true
      }
    },
  }
</script>

<template>
  <div>
    <div id="topRightBar">
      <h3 id="City">{{city}}</h3>
      <h3 id="clock">{{ clock }}</h3>
    </div>
    <div id="basicInfoContainer">
      <h3 id="temperatureInfo">{{temperature }} °C</h3>
      <div style="display: flex; flex-direction: row; align-items: center;">
        <div>
          <img :src="this.icon" alt ="icon" style="float">
        </div>
        <h3 id="weatherDescription">{{description}}</h3>
      </div>
    </div>
  </div>
</template>
