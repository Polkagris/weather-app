
<template>
  <div id="map" class="map">
   
  </div>
</template>

<script>


export default {
  name: 'Maps',
  props: {
    msg: String
  },
  components: {

    },
   data : {
        map: null,
        tileLayer: null,
        layers: [],
         
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
    initLayers() {},
},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#map{
height: 500px; 
}
</style>
