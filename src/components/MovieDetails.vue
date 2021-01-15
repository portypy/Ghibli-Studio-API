<template>
<div v-if="selectedMovie">
  <p>Title: {{selectedMovie.title}}</p>
  <p>Director: {{selectedMovie.director}}</p>
  <p>Year: {{selectedMovie.release_date}}</p>
  </div>
</template>

<script>
export default {
    name: 'movies-details',
    props: ['selectedMovie']

}
</script>

<style>

</style>