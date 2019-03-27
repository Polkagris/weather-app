<template>
  <div class="hello">

    <div class="row">
      <div class="col-md-12">
        <h1>{{ msg }}</h1>
          <h3>Cities</h3>
            <div id="buttonContainer">
              <button class="btn btn-light button" v-on:click="updateWeather('Oslo'), updateForecast('Oslo')">Oslo</button>
              <button class="btn btn-light button" v-on:click="updateWeather('Bergen'), updateForecast('Bergen')">Bergen</button>
              <button class="btn btn-light button" v-on:click="updateWeather('Stavanger'), updateForecast('Stavanger')">Stavanger</button>
              <button class="btn btn-light button" v-on:click="updateWeather('Trondheim'), updateForecast('Trondheim')">Trondheim</button>
              <button class="btn btn-light button" v-on:click="updateWeather('Kristiansand'), updateForecast('Kristiansand')">Kristiansand</button>
            </div>
      </div>
    </div>




    <div class="row">
      <div class="col-md-12">
        <div class="card">
        <h3>Current Weather in {{ infoCurrent.data.location.name }}</h3>
          <ul>
            <li>
                {{ infoCurrent.data.current.condition.text }}
                <img :src="infoCurrent.data.current.condition.icon">
            </li>
          </ul>
        </div>
      </div>
    </div>


    <div class="row">
      <div class="col-md-12">
        <h3>Forecast for {{infoCurrent.data.location.name}} </h3>
        <div id="forecasts" >
          
            <li id="singleForecast" v-for="day in infoForecast.data.forecast.forecastday">
              <div class="card">
                {{day.date}}
                {{day.day.condition.text}}
                <img :src="day.day.condition.icon" style="width: 3rem;">
            </div>
            </li>
        </div>
      </div>
    </div>
    
    
    
    
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
#forecasts{
  display: flex;
  flex-wrap: wrap;
}
#singleForecast{
  width: 15%;
}
#buttonContainer{
    display: flex;
    flex-wrap: wrap;
}
.button{
  flex: 1 1 0;
}
</style>
