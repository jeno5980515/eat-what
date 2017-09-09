<template>
  <div class="hello">
    <div>{{msg}}</div>
    <div ref="map"></div>
  </div>
</template>

<script>
import GoogleMapsLoader from 'google-maps'
// GoogleMapsLoader.KEY = 'AIzaSyA-i1a4LSmgEqupl1dCUbi8Z9ObWMQym24'
GoogleMapsLoader.LIBRARIES = ['geometry', 'places']

const shuffle = (array) => {
  let newArray = array.slice()
  let currentIndex = newArray.length
  let temporaryValue
  let randomIndex
  while (currentIndex !== 0) {
    randomIndex = Math.floor(Math.random() * currentIndex)
    currentIndex -= 1
    temporaryValue = newArray[currentIndex]
    newArray[currentIndex] = newArray[randomIndex]
    newArray[randomIndex] = temporaryValue
  }
  return newArray
}

// keyword

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Please open GPS.'
    }
  },
  mounted: function () {
    let location = {}
    navigator.geolocation.getCurrentPosition((position) => {
      const { latitude, longitude } = position.coords
      location = {
        lat: latitude,
        lng: longitude
      }
      const map = this.$refs.map
      const updateRestaurant = this.updateRestaurant
      GoogleMapsLoader.load(function (google) {
        const service = new google.maps.places.PlacesService(map)
        service.nearbySearch({
          location,
          openNow: true,
          radius: 500,
          type: ['restaurant']
        }, (resp) => {
          updateRestaurant(resp)
        })
      })
    })
  },
  methods: {
    updateRestaurant (restaurants) {
      console.log(restaurants)
      if (restaurants.length) {
        const shuffled = shuffle(restaurants)
        this.msg = shuffled[0].name
      } else {
        this.msg = 'not found'
      }
    }
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
