<template>

    <div >
        <!--<ul>
            <li><a href="#">{{ fiveDayForecast.data.location.name}}</a></li>
        </ul>
        <h1>test</h1>-->
    </div>

</template>

<script>

import axios from 'axios'

export default {
    name: 'Forecasts',
    props: {

    },
    created () {

    },
    mounted () {
    this.urlForecast = 
    'http://api.apixu.com/v1/forecast.json?key=d669f00ce9574e84ad695232192603&q=Oslo&days=5';
        axios
          .get(this.urlForecast)
          .then(response => (this.fiveDayForecast = response))
  },
    methods: {

    }
}


</script>