<template  lang="html">
<div id="main-container">
  <div id="list" class="grid-element">
          <img src="./assets/logo.svg" alt="studio ghibli" height="70">
          <h3>Movies List:</h3>
          <movies-list :movies="movies"></movies-list> 
  </div>
  <div id="tenor" class="grid-element">
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
            <img src="./assets/tenor.gif" alt="tenor gif"  height="500" id="tenor-gif">
        </div>
  </div>
    <movie-details id="movieDetails" class="grid-element" :selectedMovie="selectedMovie"></movie-details>
    <div id="tenor2" class="grid-element" >
          <maps id="maps"> </maps>
    </div>
    <charts v-if="selectedMovie" :selectedMovie="selectedMovie" id="charts" ></charts>
  </div>  
  
</template>

<script>
import { eventBus } from './main'
import MoviesList from './components/MoviesList'
import MovieDetails from './components/MovieDetails'
import ExtraDetails from './components/ExtraDetails'
import Maps from './components/Maps'
import GoogleCharts from './components/GoogleCharts'
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
      hum_nr: 0,
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
      this.hum_nr = 0
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
  "extra-details": ExtraDetails,
  "maps": Maps,
  "charts": GoogleCharts
}
}

</script>

<style lang="css" scoped>
#main-container {
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  display: grid;
  grid-template-columns: 30% 30% auto;
  grid-template-rows: 50 auto;
  background-color: rgb(24, 171, 233);
}
.grid-element{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}
#tenor{
  grid-column: 1 ;
  grid-row: 1 / span 2;
  padding-top: 2em;
  margin-left: 10em;
  justify-content: flex-start;
  align-items: flex-start;
}
#tenor2{
  grid-column: 3;
  grid-row: 2;
  padding: 4%;
}
#list{
  cursor: pointer;
  grid-column: 2;
  grid-row: 1;
  padding: 4%;
}
#movieDetails{
  grid-column: 3 ;
  grid-row: 1;
  padding-top: 3%;
  padding-right: 3%;
}
#maps{
  grid-column: 2;
  grid-row: 2;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
#charts{
  grid-column: 2;
  grid-row: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
}
#tenor-gif{
  margin-top: 4em;
    border: 3px solid green;
    block-size: auto;
}
#susu{
  box-shadow:  0 0 100px brown;
}
#susu-box{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
}
</style>
