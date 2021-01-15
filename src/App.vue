<template lang="html">
  <div>
    <movies-list :movies="movies"></movies-list>
    <movie-details :selectedMovie="selectedMovie"></movie-details>
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

<style>

</style>
