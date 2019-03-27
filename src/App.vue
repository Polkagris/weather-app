<template>
  <div id="app">
    <link href="https://fonts.googleapis.com/css?family=Quicksand" rel="stylesheet">
    <div class="container">

      <div class="row">
          <div class="col-md-6 col-sm-6">
            <Maps/>
          </div>

          <div class="col-md-6 col-sm-6">
            <HelloWorld msg="Weather App"/>
          </div>
        </div>

      <div class="row">
          <div class="col-md-12 col-sm-6">
            <Forcasts/>
          </div>
        </div>


      </div>
    </div>
    

</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Maps from './components/Maps.vue'
import Forcasts from './components/Forcasts.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Maps,
    Forcasts
    
  }
}
</script>

<style>
#app {
  font-family: 'Quicksand', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
