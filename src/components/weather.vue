<template>
  <div id="main" class="grid">
    <div class="grid-item datetime">
      {{  moment().format('MMMM Do YYYY, h:mm:ss a') }}
    </div>
    <div class="grid-item location">{{ weather_data.name }}</div>
    <div class="grid-item graphic">
      <img src="../assets/main-graphic.svg" alt="main-graphic">
    </div>
    <div class="grid-item temperature">
      <h3>{{ temperature }}<sup>&deg;C</sup></h3>
    </div>
    <div class="grid-item prediction">{{ description }}</div>
  </div>
</template>

<script>
import axios from 'axios'
import moment from "moment"

export default {
  data () {
    return {
      weather_data: {},
      temperature: 0,
      description: "",
      moment: moment
    }
  },
  methods: {
    fetch_data: function() {
      axios.get("https://api.openweathermap.org/data/2.5/find?q=Paris&units=metric&appid=dfe15a41201d660911d013203832e676")
           .then(response => {this.weather_data = response.data.list[0]})
    }
  },
  watch: {
    weather_data: function(val) {
      this.temperature = Math.round(val.main.temp)
      this.description = val.weather[0].description
    }
  },
  mounted: function(){
    this.$nextTick(function(){
      this.fetch_data()
    });
  }
}
</script>

<style>

</style>
