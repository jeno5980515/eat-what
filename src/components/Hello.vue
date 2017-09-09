<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
import GoogleMapsLoader from 'google-maps'
GoogleMapsLoader.KEY = 'AIzaSyA-i1a4LSmgEqupl1dCUbi8Z9ObWMQym24'

GoogleMapsLoader.load(function (google) {
  console.log(google)
})

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
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
