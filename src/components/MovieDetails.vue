<template lang="html">
<div>
    <div v-if="selectedMovie">
        <p>Title: {{selectedMovie.title}}</p>
        <p>Director: {{selectedMovie.director}}</p>
        <p>Year: {{selectedMovie.release_date}}</p>
        <p>{{selectedMovie.description}}</p>
        <p v-on:click.prevent="handleClickLocations" class="list-item" >Check locations </p>
        
        <!-- <p class="list-item">Check people</p>
        <p class="list-item"> Check vehicles</p> -->
    </div>
    <!-- <div v-else-if="locations">
        <ul v-for='location in locations' :location="location">
            <li>{{location.name}}</li>
        </ul>
        </div> -->
    <div v-else >
        <img src="../assets/download.png" alt="studio ghilbi logo">
    </div>
</div>
</template>

<script>
import { eventBus } from '../main'
export default {
    name: 'movies-details',
    props: ['selectedMovie'],
    // data(){
    //     return {
    //         locations: [],
    //     }
    // },
    
        
    
    methods: {
        
        handleClickLocations() {
            eventBus.$emit('locations', 1)
            // if (this.locations.length == 0) {              
            //     fetch(this.selectedMovie.locations)
            //     .then(res => res.json())
            //     .then(locations => this.locations = locations); 
            // }
        
            
        }
    }  
}

</script>

<style lang="css" scoped>
.list-item:hover {
    color: whitesmoke;
    cursor: pointer;
}
</style>