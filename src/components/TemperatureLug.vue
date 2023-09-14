<template>
  <div class="lug">
    <h2>Current Temp</h2>
    <h1>
      <div>
      <span class="material-symbols-outlined">
thermometer
      </span></div><div>{{ weather?.main?.temp }} <span>&#176;</span></div>
    </h1>
    <div class="secondary">
      <div>
        <h2>Min</h2>
        {{ weather?.main?.temp_min }}
      </div>
      <div>
        <h2>Max</h2>
        {{ weather?.main?.temp_max }}
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'TemperatureLug',
  props: {
    weather: {}
  }
}
</script>
<style scoped>
h1 {
  margin-left: -8px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
.secondary {
  display: flex;
  justify-content: flex-start;
  
}

.secondary div {
  margin-top: 0.5em;
  margin-right: 0.5em;
}
</style>
