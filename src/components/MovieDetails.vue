<template>
<div>
    <div v-if="selectedMovie">
        <p>Title: {{selectedMovie.title}}</p>
        <p>Director: {{selectedMovie.director}}</p>
        <p>Year: {{selectedMovie.release_date}}</p>
        <p>{{selectedMovie.description}}</p>
    </div>
    <div v-else>
        <img src="../assets/download.png" alt="">

    </div>
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