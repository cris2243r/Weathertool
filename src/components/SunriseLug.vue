<template>
  <div class="lug">
    <h2>Sunrise</h2>
    <h1>{{ sunrise }}</h1>
    <h2>Sunset</h2>
    <h1>{{ sunset}}</h1>
  </div>
</template>
<script>
export default {
  name: 'SunriseLug',
  props: {
    weather: {}
  },
  computed: {
    sunrise() {
      return this.formatTime(this.weather?.sys?.sunrise)
    },
    sunset() {
      return this.formatTime(this.weather?.sys?.sunset)
    }
  },
  methods: {
    formatTime(timestamp) {

      let unix_timestamp = timestamp
// Create a new JavaScript Date object based on the timestamp
// multiplied by 1000 so that the argument is in milliseconds, not seconds.
      const date = new Date(unix_timestamp * 1000);
// Hours part from the timestamp
      const hours = date.getHours();
// Minutes part from the timestamp
      const minutes = "0" + date.getMinutes();
// Seconds part from the timestamp
      const seconds = "0" + date.getSeconds();

// Will display time in 10:30:23 format
      const formattedTime = hours + ':' + minutes.substr(-2) + ':' + seconds.substr(-2);

      console.log(formattedTime);

      return formattedTime
    }
  },

}
</script>
<style scoped>
h1 {
  font-size: 1em;
  margin-bottom: 0.6em;
}
</style>
