<template>
  <div id="main" class="grid">
    <div class="grid-item datetime">
      Tue 23rd Feb
      <br>
      7:33 am
    </div>
    <div class="grid-item location">{{ weather_data.name }}</div>
    <div class="grid-item graphic">
      <img src="../assets/main-graphic.svg" alt="main-graphic">
    </div>
    <div class="grid-item temperature">-7</div>
    <div class="grid-item prediction">{{ weather_data.weather[0].description }}</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      weather_data: {}
    }
  },
  methods: {
    fetch_data: function() {
      axios.get("https://api.openweathermap.org/data/2.5/find?q=Paris&units=metric&appid=dfe15a41201d660911d013203832e676")
           .then(response => {this.weather_data = response.data.list[0]})
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
