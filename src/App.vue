<template>
  <div id="listAndLogo">
      <div v-if="locations.length != 0 "> 
          <extra-details :locations="locations"></extra-details>
          <extra-details></extra-details>
       </div>
      <div v-else >
          <img src="./assets/tenor.gif" alt="tenor gif" id="tenor" height="500">
      </div>
      <div id="list">
          <img src="./assets/logo.svg" alt="studio ghibli" height="70">
          <h3>Movies List:</h3>
          <movies-list :movies="movies"></movies-list>
      </div>
      <movie-details id="movieDetails" :selectedMovie="selectedMovie"></movie-details>
  </div>
</template>

<script>
import { eventBus } from './main'
import MoviesList from './components/MoviesList'
import MovieDetails from './components/MovieDetails'
import ExtraDetails from './components/ExtraDetails'
import Locations from './components/Locations'
export default {
  name: "app",
  data() {
    return {
      movies: [],
      selectedMovie: null,
      number: 0,
      locations: []
    }
  },

mounted() {
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(res => res.json())
    .then(movies => this.movies = movies);

     

    eventBus.$on('selected-movie', (movie) => {
      this.selectedMovie = movie;

    eventBus.$on('locations',(number) => {
      this.number = number;
      if (this.locations.length == 0) {              
                fetch(this.selectedMovie.locations)
                .then(res => res.json())
                .then(locations => this.locations = locations); 
            }
    })
    
    });
    
},
components: {
  "movies-list": MoviesList,
  "movie-details": MovieDetails,
  "extra-details": ExtraDetails,
  "locations": Locations
}
}
</script>

<style lang="css" scoped>
#listAndLogo {
  font-family:fantasy;
  display: grid;
  grid-template-columns: 40% 30% auto;
  background-color: rgb(24, 171, 233);
}
#tenor{
  grid-column: 1 ;
  padding: 2%;
}
#list{
  cursor: pointer;
  grid-column: 2 / 3;
}
#movieDetails{
  grid-column: 3 / 4;
  padding-top: 3%;
  padding-right: 3%;
}



  
</style>
