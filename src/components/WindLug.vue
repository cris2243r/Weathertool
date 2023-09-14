<template>
  <div class="lug">
    <h2>Wind</h2>
    <h1>{{weather?.wind?.speed}} km/h</h1>
    <div>
      <span :style="windDirection"  class="material-symbols-outlined">
navigation
</span>
    </div>
  </div>
</template>
<script>
export default {
  name: 'WindLug',
  props: {
    weather: {}
  },
  computed: {
    windDirection() {
      const rotation = this.weather?.wind?.deg | 0
      return `transform: rotate(${rotation}deg)`
    }
  },
}
</script>
<style scoped>

span {
  margin-top: 0.2em;
  font-size: 2.8em;
}


</style>
