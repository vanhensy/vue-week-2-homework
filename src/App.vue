<template>
  <div id="app">
    <weather/>
  </div>
</template>

<script>
import weather from "@/components/weather"

export default {
  name: 'app',
  components: {
    "weather": weather
  }
}
</script>