<template>
  <div id="main" class="grid">
    <div class="grid-item datetime">
      {{  moment().format('h:mm A') }}
      <br>
      {{  moment().format('MMMM Do YYYY') }}
    </div>
    <div class="grid-item location">{{ weather_data.name }}</div>
    <div class="grid-item graphic">
      <img src="../assets/main-graphic.svg" alt="main-graphic">
    </div>
    <div class="grid-item temperature">
      <h3>{{ temperature }}<sup>&deg;C</sup></h3>
    </div>
    <div class="grid-item prediction">
      <i class="wi" :class="weather_icon"></i>
      {{ description }}
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import moment from "moment"
import weather_icons from '../json/weather-icon.json'

export default {
  data () {
    return {
      weather_data: {},
      temperature: 0,
      description: "",
      weather_icon: "",
      moment: moment
    }
  },
  methods: {
    fetch_data: function() {
      let self = this
      axios.get("https://api.openweathermap.org/data/2.5/find?q=Paris&units=metric&appid=dfe15a41201d660911d013203832e676")
           .then(function(response) {
             self.weather_data = response.data.list[0]
             self.weather_icon = self.fetch_weather_icon(self.weather_data.weather[0].id)
            })
    },
    fetch_weather_icon: function(code) {
      var prefix = 'wi wi-';
      var icon = weather_icons[code].icon;

      // If we are not in the ranges mentioned above, add a day/night prefix.
      if (!(code > 699 && code < 800) && !(code > 899 && code < 1000)) {
        icon = 'day-' + icon;
      }

      // Finally tack on the prefix.
      return icon = prefix + icon;
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
      this.fetch_data();
    });
  }
}
</script>

<style>

</style>
