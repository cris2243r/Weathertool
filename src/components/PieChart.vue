<template>
<!--  <div>{{weather?.main?.humidity}}%</div>-->
  <div class="pie" :style="pieStyle">{{weather?.main?.humidity}}%</div>
</template>
<script>
export default {
  name: 'PieChart',
  props: {
    weather: {}
  },
  computed: {
    pieStyle() {
      return `--p:${this.weather?.main?.humidity};--b:10px;--c:#efb41d;`
    }
  },
}
</script>
<style scoped>
.pie {
  --w:80px;

  width: var(--w);
  aspect-ratio: 1;
  position: relative;
  display: inline-grid;
  place-content: center;
  margin: 5px;
  font-size: 25px;
  font-weight: bold;
  font-family: sans-serif;
}
.pie:before {
  content: "";
  position: absolute;
  border-radius: 50%;
  inset: 0;
  background:
      radial-gradient(farthest-side,var(--c) 98%,#0000) top/var(--b) var(--b) no-repeat,
      conic-gradient(var(--c) calc(var(--p)*1%),#0000 0);
  -webkit-mask:radial-gradient(farthest-side,#0000 calc(99% - var(--b)),#000 calc(100% - var(--b)));
  mask:radial-gradient(farthest-side,#0000 calc(99% - var(--b)),#000 calc(100% - var(--b)));
}

.pie:before {

}
</style>
