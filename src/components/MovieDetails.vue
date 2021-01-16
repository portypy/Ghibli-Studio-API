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
        <p class="list-item" v-on:click="handleClickLocations" >Check locations </p>   
        <p class="list-item" v-on:click="handleClickHumans">Check people</p>
        <p class="list-item" v-on:click="handleClickVehicles"> Check vehicles</p>
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
        },
        handleClickHumans(){
            eventBus.$emit('humans')
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