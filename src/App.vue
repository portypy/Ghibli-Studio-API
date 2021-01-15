<template>
  <div>
    <p>hi</p>
  </div>
</template>

<script>
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
}
}
</script>

<style>

</style>
