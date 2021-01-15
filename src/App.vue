<template>
  <div>
    <movies-list :movies="movies"></movies-list>
  </div>
</template>

<script>
import MoviesList from './components/MoviesList'
export default {
  name: "app",
  data() {
    return {
      movies: []
    }
  },

mounted() {
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(res => res.json())
    .then(movies => this.movies = movies)
},
components: {
  "movies-list": MoviesList
}
}
</script>

<style>

</style>
