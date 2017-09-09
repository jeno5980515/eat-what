<template>
  <div class="hello">
    <div ref="map"></div>
  </div>
</template>

<script>
import GoogleMapsLoader from 'google-maps'
GoogleMapsLoader.KEY = 'AIzaSyA-i1a4LSmgEqupl1dCUbi8Z9ObWMQym24'
GoogleMapsLoader.LIBRARIES = ['geometry', 'places']

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted: function () {
    const map = this.$refs.map
    GoogleMapsLoader.load(function (google) {
      const service = new google.maps.places.PlacesService(map)
      service.nearbySearch({
        location: {lat: -33.867, lng: 151.195},
        radius: 500,
        type: ['store']
      }, (resp) => {
        console.log(resp)
      })
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
