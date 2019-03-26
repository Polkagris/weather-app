<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <h3>Current Weather</h3>
    <ul>
      <li>
          Location: {{ info.data.location.name }} 
      </li>
      <li>
          Weather: {{ info.data.current.condition.text }}
      </li>
    </ul>
    <h3>Cities</h3>
    <ul>
      <li><a href="#" v-on:click="updateWeather('Oslo')">Oslo</a></li>
      <li><a href="#" v-on:click="updateWeather('Bergen')">Bergen</a></li>
      <li><a href="#" v-on:click="updateWeather('Stavanger')">Stavanger</a></li>
      <li><a href="#" v-on:click="updateWeather('Trondheim')">Trondheim</a></li>
      <li><a href="#" v-on:click="updateWeather('Kristiansand')">Kristiansand</a></li>
    </ul>
    
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    info: null,
    base: 'Oslo',
    url: ""
  },
  created () {
        this.url = 'http://api.apixu.com/v1/current.json?key=d669f00ce9574e84ad695232192603&q=Oslo';
      axios
        .get(this.url)
        .then(response => (this.info = response))
    },
    methods: {
      updateWeather(City){
        this.base = City
        this.url = 'http://api.apixu.com/v1/current.json?key=d669f00ce9574e84ad695232192603&q=' + this.base;
        axios
          .get(this.url)
          .then(response => (this.info = response))
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
