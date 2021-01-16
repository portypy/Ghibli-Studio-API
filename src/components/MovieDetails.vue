<template lang="html">
<div>
    <div v-if="selectedMovie">
        <p>Title: {{selectedMovie.title}}</p>
        <p>Director: {{selectedMovie.director}}</p>
        <p>Year: {{selectedMovie.release_date}}</p>
        <p>{{selectedMovie.description}}</p>
        
    </div>
    
    <div v-else >
        <img src="../assets/download.png" alt="studio ghilbi logo">
    </div>
    <div>
        <p v-on:click="handleClickLocations" class="list-item" >Check locations </p>
        
        <p class="list-item">Check people</p>
        <p v-on:click="handleClickVehicles" class="list-item"> Check vehicles</p>
    </div>
</div>
</template>

<script>
import { eventBus } from '../main'
export default {
    name: 'movies-details',
    props: ['selectedMovie'],
    methods: {
        handleClickLocations() {
            eventBus.$emit('locations'); 
        },
        handleClickVehicles(){
            eventBus.$emit('vehicles')
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