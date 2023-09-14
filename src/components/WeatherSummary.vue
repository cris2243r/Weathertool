<template>
  <div id="weather-summary">
    <ConditionsLug :icon-source="iconSource" :weather="weather"/>
    <TemperatureLug :weather="weather"/>
    <HumidityLug :weather="weather"/>
    <WindLug :weather="weather"/>
    <SunriseLug :weather="weather"/>
  </div>
</template>
<script>
import ConditionsLug from "@/components/ConditionsLug";
import TemperatureLug from "@/components/TemperatureLug";
import HumidityLug from "@/components/HumidityLug";
import SunriseLug from "@/components/SunriseLug";
import WindLug from "@/components/WindLug";

export default {
  name: 'WeatherSummary',
  components: {SunriseLug, HumidityLug, TemperatureLug, ConditionsLug, WindLug},
  props: {
    weather: {}
  },
  computed: {
    iconSource() {
      return `http://openweathermap.org/img/wn/${this.weather?.weather[0].icon}@2x.png`
    }
  },
}
</script>
<style>

#weather-summary {
  /*height: 6em;*/
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding-left: 1em;
  padding-right: 2em;
  width: 80vw;
  margin: auto;
}

@media only screen and (max-width: 768px) {
  #weather-summary {
    flex-direction: column;
    margin: unset;
  }
}

h1 {
  margin-top: 0;
  margin-bottom: 0;
  text-align: left;
  display: flex;
}

.lug h2 {
  margin-top: 0;
  margin-bottom: 0.5em;
  font-size: 0.8em;
  text-align: left;
}

.lug h1 {
  font-size: 1.2em;
}

h4 {
  text-align: left;
  width: 100%;
}

.lug {
  border-radius: 0.5em;
  padding-left: 10px;
  padding-right: 10px;
  padding-top: 10px;
  background-color: #90959e;
  color: #ffffff;
  width: 300px;
  margin-right: 1em;
  height: 8em;
}


@media only screen and (max-width: 768px) {
}

</style>
