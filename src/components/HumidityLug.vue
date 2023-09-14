<template>
  <div class="lug">
    <h2>Humidity</h2>
    <PieChart :weather="weather"/>
  </div>
</template>
<script>
import PieChart from "@/components/PieChart";

export default {
  name: 'HumidityLug',
  components: {PieChart},
  props: {
    weather: {}
  }
}
</script>
