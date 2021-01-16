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
        <div v-if="veh_nr != 0">
            <extra-details :vehicles="vehicles "></extra-details> 
        </div>
        <div v-else-if="loc_nr != 0 "> 
            <extra-details :locations="locations "></extra-details> 
        </div>
        <div v-else-if="hum_nr !=0">
          <extra-details :humans="humans "></extra-details>
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
export default {
  name: "app",
  data() {
    return {
      movies: [],
      selectedMovie: null,
      locations: [],
      vehicles: [],
      humans: [],
      loc_nr: 0,
      veh_nr: 0,
      hum_nr: 0
    }
  },

mounted() {
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(res => res.json())
    .then(movies => this.movies = movies);

    eventBus.$on('selected-movie', (movie) => {
      this.selectedMovie = movie;
      this.loc_nr = 0
      this.veh_nr = 0
    }),
    eventBus.$on('locations',() => {
      this.loc_nr = 1
      if (this.locations.length == 0) {              
                fetch('https://ghibliapi.herokuapp.com/locations/')
                .then(res => res.json())
                .then(locations => this.locations = locations)
            }
      this.hum_nr = 0
      this.veh_nr = 0
      this.selectedMovie = null
    }),
    eventBus.$on('vehicles',() => {
      this.veh_nr = 1
      if (this.vehicles.length == 0) {              
                fetch("https://ghibliapi.herokuapp.com/vehicles/")
                .then(res => res.json())
                .then(vehicles => this.vehicles = vehicles)
            }  
      this.hum_nr = 0
      this.loc_nr = 0
      this.selectedMovie = null
    }),
    eventBus.$on('humans',() => {
      this.hum_nr = 1
      if (this.humans.length == 0) {
        fetch("https://ghibliapi.herokuapp.com/people/")
        .then(res => res.json())
        .then(humans => this.humans = humans)
      }
      this.veh_nr = 0
      this.loc_nr = 0
      this.selectedMovie = null
    })
},
components: {
  "movies-list": MoviesList,
  "movie-details": MovieDetails,
  "extra-details": ExtraDetails
}
}
</script>

<style lang="css" >
#main-container {
  font-family:fantasy;
  display: grid;
  grid-template-columns: 40% 20% auto;
  grid-template-rows: 90 auto;
  background-color: rgb(24, 171, 233);
}
#tenor{
  grid-column: 1 ;
  grid-row: 1;
  padding: 2%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}
#list{
  cursor: pointer;
  grid-column: 2;
  grid-row: 1;
}
#movieDetails{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  grid-column: 3 ;
  grid-row: 1;
  padding-top: 3%;
  padding-right: 3%;
}

</style>
