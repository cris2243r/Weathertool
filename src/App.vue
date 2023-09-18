<template>
  <div id="app"> 
    <header>
    <h1>
      WeatherTool
    </h1>
    <form>
      <fieldset>
        <label for="query"> <h4>Select a city</h4></label>
        <input id="query" type="text" autocomplete="off" placeholder="Enter city...." @keyup="refreshCities" v-model="query">
      </fieldset>
      <input
          type="button" @click="clearQuery" value="X">
    </form>
    <ul class="results">
      <li v-for="(city, idx) in cities" :key="'part-' + idx" @click="setCity(city)">{{ city.name }}, {{ city.state }},
        {{ city.country }}
      </li>
    </ul>
    </header>
   <!-- Wrap the following content within a transition -->
   <transition name="slide">
      <div class="selected-city" v-if="selectedCity">
        <h2>Current Weather for <strong>{{ selectedCity?.name }} {{ selectedCity?.state }} {{ selectedCity?.country }}</strong></h2>
        <div>
          <WeatherSummary :weather="weather"/>
        </div>
      </div>
    </transition>
    <transition name="fade">
    <div class="empty" v-if="!selectedCity">
      <span class="material-symbols-outlined">cloud_off</span>
      <h1>Search for a city to begin</h1>
    </div>
    </transition>
  </div>
</template>

<script>

import WeatherSummary from "@/components/WeatherSummary";

export default {
  name: 'App',
  components: {WeatherSummary},
  data() {
    return {
      cities: [],
      selectedCity: null,
      weather: null,
      units: 'metric',
      query: null,
    }
  },
  methods: {

    async refreshCities() {
  console.log("refreshing cities");
  console.log(this.query);

  // Check if the query is empty before making the API request
  if (this.query.trim() === "") {
    this.cities = [];
    return; // Exit the function if query is empty
  }

  const cityData = await fetch(`https://api.openweathermap.org/geo/1.0/direct?q=${this.query}&limit=5&appid=bf89e941da14d9a5e0a60764ed99bf4a`)
  
  // Handle the response status
  if (cityData.ok) {
    this.cities = await cityData.json();
  } else {
    console.error("Failed to fetch city data:", cityData.status);
  }
},

    async refreshWeatherData() {
      const url =
          `https://api.openweathermap.org/data/2.5/weather?lat=${this.selectedCity.lat}&lon=${this.selectedCity.lon}&appid=bf89e941da14d9a5e0a60764ed99bf4a&units=${this.units}`
      const weatherData = await fetch(url)
      this.weather = await weatherData.json()
      console.log(url)
    },

    setCity(city) {
      this.selectedCity = city;
      this.cities = []
    },

    clearQuery() {
      this.query = null
      this.setCity(null)
    }


  },
  watch: {
    selectedCity(newval) {
      newval ? this.refreshWeatherData() : this.weather = null
    }
  },
}
</script>

<style>
#app {
  font-family: Playfair, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #efefef;
}

body {
  margin: 0 0 0 0 ;
  background-color: #000000;
}

header {
  background-color: #eae7dc;
  color:rgb(0, 0, 0);
  padding-top: 1em;
  padding-bottom: 1em;
  display: flex;
  flex-direction: column;
  align-items: center;
}

header h1 {
  font-size: 4.5em;
  margin-bottom: 0.7em;
  margin-top: 0.7em;
}


form {
  text-align: left;
  display: flex;
  justify-content: center;
  align-items: center;
}

fieldset {
  display: flex;
  flex-direction: column;
  border: none;
}

label {
  padding-bottom: 0.7em;
}

input::placeholder {
  color: #000000;
}


input[type=text] {
  padding-left: 0.9em;
  width:100%;
  height: 3.5em;
  font-size: 1.3em;
  font-weight: bold;
  border-radius: 20px;
  border-color:#f6767600;
  outline: none;
  margin-left: 0.2em;
  color: #000000;
  background-color: #eae7dc;
  border-color: #000000;
}

input[type=button] {
  background-color: transparent;
  border: none;
  color: rgb(0, 0, 0);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  font-weight: bold;
  font-size: 2em;
  margin-top: -2.5em;
  margin-left: -0.5em;
  outline: none;
 
}
/* Add CSS for better mobile appearance */
@media only screen and (max-width: 768px) {
  input[type=text] {
    height: 3.5em;
    font-size: 1.3em;
    padding-left: 0.9em;
    padding-right: 1.2em;
    margin-left: 0.7em;
  }
}

input[type=button]:hover {
  cursor: pointer;
  color: #b41414;
}

ul {
  margin-top: 1em;
  list-style: none;
}

li {
  padding-bottom: 0.2em;
}
@media only screen and (max-width: 768px) {
  li {
    font-size: 1.6em; 
  }
}

li:hover {
  cursor: pointer;
  font-weight: bold;
}

.empty {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 3em;
  color: #ffffff;
  font-size: 1.6em;
  font-weight: bold;
}

.empty span{
  font-size: 5em;
}


h1 {
  margin-top: 0;
  margin-bottom: 0;
  text-align: left;
  display: flex;
  font-size: 1em;
}

.lug h1 {
    font-size: 1.5em;
}
.secondary[data-v-ec94e9cc] {
    display: flex;
    justify-content: flex-start;
    font-size: 1.4em;
}

h2 {
  margin-top: 1em;
  margin-bottom: 1em;
  font-size: 3em;
  text-align: center;
  color: rgb(255, 255, 255)
}

h4 {
  text-align: center;
  width: 100%;
  font-size: 3em;
  margin-left: 0.em;

}



@media only screen and (max-width: 768px) {
  .lug {
    margin-bottom: 0.8em;
    width: calc(100vw - 3.2em);
  }
}
.slide-enter-active,
.slide-leave-active {
  transition: transform 0.5s ease-in-out;
}

.slide-enter,
.slide-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}
</style>
