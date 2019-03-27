
<template>
<div>
  <div id="map" class="map">

  </div>
  <div id="container">
    <button class="btn btn-info" v-on:click="changeLocation(60.39299, 5.32415)">Bergen</button>
    <button class="btn btn-info" v-on:click="changeLocation(63.43049, 10.39506)">Trondheim</button>
    <button class="btn btn-info" v-on:click="changeLocation(59.91273, 10.74609)">Oslo</button>
    <button class="btn btn-info" v-on:click="changeLocation(58.97005, 5.73332)">Stavanger</button>
    <button class="btn btn-info" v-on:click="changeLocation(58.14671, 7.9956)">Kristiansand</button>
 </div>
</div>
</template>

<script>
//import HelloWorld from './HelloWorld.vue'

export default {
  name: 'Maps',
  props: {
    msg: String
  },
  components: {

    },
   data()  {
        return {map: null,
        tileLayer: null,
        layers: [],
        }
  },
  mounted() {
  this.initMap();
  this.initLayers();
},
  methods: {
    initMap() {
        this.map = L.map('map').setView([59.91273, 10.74609],10);

        this.tileLayer = L.tileLayer(
        'https://cartodb-basemaps-{s}.global.ssl.fastly.net/rastertiles/voyager/{z}/{x}/{y}.png',
        {
            maxZoom: 18,
            attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, &copy; <a href="https://carto.com/attribution">CARTO</a>',
        }
        );
        this.tileLayer.addTo(this.map);
        
    },
    initLayers() {
        const marker = L.marker([59.91273, 10.74609]);
        marker.bindPopup("<b>Hello world!</b><br>I am a popup.").openPopup();
        marker.addTo(this.map);
    },

    changeLocation(lat, lon) {
        this.map.flyTo([lat, lon],10);
    }
},
}
</script>

<style scoped>
#map{
height: 500px; 
}

#container{
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
}

</style>
