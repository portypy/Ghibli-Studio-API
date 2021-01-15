<template>
  <div id="listAndLogo">
      <img src="./assets/tenor.gif" alt="tenor gif" id="tenor" height="500">
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
export default {
  name: "app",
  data() {
    return {
      movies: [],
      selectedMovie: null
    }
  },

mounted() {
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(res => res.json())
    .then(movies => this.movies = movies);

    
    eventBus.$on('selected-movie', (movie) => {
      this.selectedMovie = movie;
      console.log("selected in app",this.selectedMovie);

    });
},
components: {
  "movies-list": MoviesList,
  "movie-details": MovieDetails
}
}
</script>

<style lang="css" scoped>
#listAndLogo {
  display: grid;
  grid-template-columns: 40% 30% auto;
  background-color: rgb(24, 171, 233);
}
#tenor{
  grid-column: 1 ;
}
#list{
  cursor: pointer;
  grid-column: 2 / 3;
}
#movieDetails{
  grid-column: 3 / 4;
  padding-top: 3%;
}



  
</style>
