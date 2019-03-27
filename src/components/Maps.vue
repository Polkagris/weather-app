
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
        this.map = L.map('map').setView([61.91273, 10.74609],5);

        this.tileLayer = L.tileLayer(
        'https://cartodb-basemaps-{s}.global.ssl.fastly.net/rastertiles/voyager/{z}/{x}/{y}.png',
        {
            maxZoom: 18,
            attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, &copy; <a href="https://carto.com/attribution">CARTO</a>',
        }
        );
        this.tileLayer.addTo(this.map);

        L.marker([59.913868, 10.752245], {title: "Oslo"}).addTo(this.map);
        L.marker([63.430515, 10.395053], {title: "Trondheim"}).addTo(this.map);
        L.marker([60.391262, 5.322054], {title: "Bergen"}).addTo(this.map);
        L.marker([58.159912, 8.018206], {title: "Kristiansand"}).addTo(this.map);
        L.marker([58.969975, 5.733107], {title: "Stavanger"}).addTo(this.map);

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
.btn{
    flex: 1 1 0;
    margin: 0 1px;
}

</style>
