<template>
  <div class="lug">
    <h2>Conditons</h2>
    <h1>{{weather?.weather[0].main}}</h1>
    <img :src="iconSource" :alt="weather?.weather[0].description">
  </div>
</template>
<script>
export default {
  name: 'ConditionsLug',
  props: {
    iconSource: {},
    weather: {}
  }
}
</script>
<style scoped>

img {
  margin-top: -2em;
}
</style>
