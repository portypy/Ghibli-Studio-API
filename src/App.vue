<template>
<div id="main-container">
    <div id="list">
          <div >
              <img src="./assets/logo.svg" alt="studio ghibli" height="70">
              <h3>Movies List:</h3>
              <movies-list :movies="movies"></movies-list>
          </div>  
    </div>
    <div id="tenor">
        <div v-if="vehicles.length != 0">
            <extra-details :vehicles="vehicles "></extra-details> 
        </div>
        <div v-else-if="locations.length != 0 "> 
            <extra-details :locations="locations "></extra-details>      
        </div>
        <div v-else >
            <img src="./assets/tenor.gif" alt="tenor gif"  height="500">
        </div>
    </div>
    <movie-details id="movieDetails" :selectedMovie="selectedMovie"></movie-details>
</div>
</template>

<script>
import { eventBus } from './main'
import MoviesList from './components/MoviesList'
import MovieDetails from './components/MovieDetails'
import ExtraDetails from './components/ExtraDetails'
// import Locations from './components/Locations'
export default {
  name: "app",
  data() {
    return {
      movies: [],
      selectedMovie: null,
      locations: [],
      vehicles: []
    }
  },

mounted() {
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(res => res.json())
    .then(movies => this.movies = movies);

     

    eventBus.$on('selected-movie', (movie) => {
      this.selectedMovie = movie;
      this.locations = []
      this.vehicles = []

    }),
    eventBus.$on('locations',() => {
      if (this.locations.length == 0) {              
                fetch('https://ghibliapi.herokuapp.com/locations/')
                .then(res => res.json())
                .then(locations => this.locations = locations)
            }
      this.selectedMovie = null
      this.vehicles = []
    }),
    eventBus.$on('vehicles',() => {
      if (this.vehicles.length == 0) {              
                fetch("https://ghibliapi.herokuapp.com/vehicles/")
                .then(res => res.json())
                .then(vehicles => this.vehicles = vehicles)
            }
      this.selectedMovie = null
      this.locations =[]
    })


    
    
    
},
components: {
  "movies-list": MoviesList,
  "movie-details": MovieDetails,
  "extra-details": ExtraDetails,
  // "locations": Locations
}
}
</script>

<style lang="css" scoped>
#main-container {
  font-family:fantasy;
  display: grid;
  grid-template-columns: 40% 30% auto;
  grid-template-rows: 90 auto;
  background-color: rgb(24, 171, 233);
}
#tenor{
  grid-column: 1 ;
  grid-row: 1;
  padding: 2%;
}

#list{
  cursor: pointer;
  grid-column: 2;
  grid-row: 1;
}
#movieDetails{
  grid-column: 3 ;
  grid-row: 1;
  padding-top: 3%;
  padding-right: 3%;
}

</style>
