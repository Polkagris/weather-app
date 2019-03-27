<template>
  <div class="hello">
    <div class="row">
      <div class="col-md-12">
        <h1>{{ msg }}</h1>
        <h3>Forecasts</h3>
        <div id="buttonContainer">
          <!-- Houses the buttons that change the currently selected city to show forecasts for -->
          <button
            class="btn btn-light button"
            v-on:click="updateWeather('Oslo'), updateForecast('Oslo')"
          >Oslo</button>
          <button
            class="btn btn-light button"
            v-on:click="updateWeather('Bergen'), updateForecast('Bergen')"
          >Bergen</button>
          <button
            class="btn btn-light button"
            v-on:click="updateWeather('Stavanger'), updateForecast('Stavanger')"
          >Stavanger</button>
          <button
            class="btn btn-light button"
            v-on:click="updateWeather('Trondheim'), updateForecast('Trondheim')"
          >Trondheim</button>
          <button
            class="btn btn-light button"
            v-on:click="updateWeather('Kristiansand'), updateForecast('Kristiansand')"
          >Kristiansand</button>
        </div>
      </div>
    </div>

    <div class="row">
      <!-- Prints out weather and location name for the currently chosen city -->
      <div class="col-md-12">
        <div class="card">
          <h3>Current Weather in {{ infoCurrent.data.location.name }}</h3>
          <ul>
            <li>
              {{ infoCurrent.data.current.condition.text }}
              <img
                :src="infoCurrent.data.current.condition.icon"
              >
            </li>
          </ul>
        </div>
      </div>
    </div>

    <div class="row">
      <!-- Creates cards for each forecast for 5 days from the current date for the chosen city -->
      <div class="col-md-12 col-sm-12">
        <h3>Forecast for {{infoCurrent.data.location.name}}</h3>
        <div id="forecasts">
          <li
            id="singleForecast"
            class="card"
            v-for="day in infoForecast.data.forecast.forecastday"
          >
            <img :src="day.day.condition.icon" style="width: 3rem;">
            {{day.date}}
            {{day.day.condition.text}}
          </li>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
    infoCurrent: null,
    infoForecast: null,
    base: "Oslo",
    fore: "Oslo",
    urlCurrent: "",
    urlForecast: ""
  },
  created() {
    this.urlCurrent =
      "http://api.apixu.com/v1/current.json?key=d669f00ce9574e84ad695232192603&q=Oslo";
    axios.get(this.urlCurrent).then(response => (this.infoCurrent = response));
  },
  mounted() {
    this.urlForecast =
      "http://api.apixu.com/v1/forecast.json?key=d669f00ce9574e84ad695232192603&q=Oslo&days=5";
    axios
      .get(this.urlForecast)
      .then(response => (this.infoForecast = response));
  },
  methods: {
    updateWeather(City) {
      // Gets the current weather for a chosen city
      this.base = City;
      this.urlCurrent =
        "http://api.apixu.com/v1/current.json?key=d669f00ce9574e84ad695232192603&q=" +
        this.base;
      axios
        .get(this.urlCurrent)
        .then(response => (this.infoCurrent = response));
    },
    updateForecast(City) {
      // Gets the forecast for the next 4 days in addition to the forecast for the current day for the chosen city(as forecasts may differ from the actual weather)
      this.fore = City;
      this.urlForecast =
        "http://api.apixu.com/v1/forecast.json?key=d669f00ce9574e84ad695232192603&q=" +
        this.fore +
        "&days=5";
      axios
        .get(this.urlForecast)
        .then(response => (this.infoForecast = response));
    }
  }
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#forecasts {
  display: flex; /* Makes the app scale for phones */
  flex-wrap: wrap;
  align-items: stretch;
}
#singleForecast {
  flex: 1 1 0;
  min-width: 50px;
}
#singleCard {
  flex: 1 1 0;
}

#buttonContainer {
  display: flex;
  flex-wrap: wrap;
}
.button {
  flex: 1 1 0;
}
</style>
