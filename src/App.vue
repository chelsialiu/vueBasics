<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Coming Soon: Near-Earth Objects"/> -->
    <AsteroidGrid  @remove="remove" :asteroids="asteroids" header="Near-Earth Objects" />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import AsteroidGrid from './components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    // HelloWorld
    AsteroidGrid
  },
  data() {
      return {
        asteroids: []
      }
    },            
    created: function () {
        this.fetchAsteroids();
    },
    methods: {
        fetchAsteroids: function () {
            var apiKey = 'lkgI9to0hRizfzk4xTAxtNTTFkkA4Mtq7y1yW5me';
            var url = 'https://api.nasa.gov/neo/rest/v1/neo/browse?api_key=' + apiKey;
            axios.get(url)
                .then(res => {                                       
                    this.asteroids = res.data.near_earth_objects.slice(0, 10);
                });
        },
        remove: function (index) {
            this.asteroids.splice(index, 1);
        },
    }
}
</script>

<style>
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
  [v-cloak] {
      display: none;
  }
</style>
