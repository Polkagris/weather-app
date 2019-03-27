<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <h3>Current Weather in {{ infoCurrent.data.location.name }}</h3>
    <ul>
      <li>
          {{ infoCurrent.data.current.condition.text }}
          <img :src="infoCurrent.data.current.condition.icon">
      </li>
    </ul>
    <h3>Forecast for {{infoCurrent.data.location.name}} </h3>
    <li v-for="day in infoForecast.data.forecast.forecastday">
        {{day.date}}
        {{day.day.condition.text}}
        <img :src="day.day.condition.icon">
      </li>
    <h3>Cities</h3>
    <ul>
      <li><a href="#" v-on:click="updateWeather('Oslo'), updateForecast('Oslo')">Oslo</a></li>
      <li><a href="#" v-on:click="updateWeather('Bergen'), updateForecast('Bergen')">Bergen</a></li>
      <li><a href="#" v-on:click="updateWeather('Stavanger'), updateForecast('Stavanger')">Stavanger</a></li>
      <li><a href="#" v-on:click="updateWeather('Trondheim'), updateForecast('Trondheim')">Trondheim</a></li>
      <li><a href="#" v-on:click="updateWeather('Kristiansand'), updateForecast('Kristiansand')">Kristiansand</a></li>
    </ul>
    
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    infoCurrent: null,
    infoForecast: null,
    base: 'Oslo',
    fore: 'Oslo',
    urlCurrent: "",
    urlForecast: ""
  },
  created () {
        this.urlCurrent = 'http://api.apixu.com/v1/current.json?key=d669f00ce9574e84ad695232192603&q=Oslo';
      axios
        .get(this.urlCurrent)
        .then(response => (this.infoCurrent = response))
    },
  mounted () {
    this.urlForecast = 'http://api.apixu.com/v1/forecast.json?key=d669f00ce9574e84ad695232192603&q=Oslo&days=5';
        axios
          .get(this.urlForecast)
          .then(response => (this.infoForecast = response))
  },
    methods: {
      updateWeather(City){
        this.base = City
        this.urlCurrent = 'http://api.apixu.com/v1/current.json?key=d669f00ce9574e84ad695232192603&q=' + this.base;
        axios
          .get(this.urlCurrent)
          .then(response => (this.infoCurrent = response))
      },
      updateForecast(City){
        this.fore = City
        this.urlForecast = 'http://api.apixu.com/v1/forecast.json?key=d669f00ce9574e84ad695232192603&q=' + this.fore + '&days=5';
        axios
          .get(this.urlForecast)
          .then(response => (this.infoForecast = response))

      }
    }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
</style>
