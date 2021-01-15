<template lang="html">
  <li v-on:click="handleClick"> {{movie.title}}</li>
</template>

<script>
import { eventBus } from '../main'
export default {
    name: 'list-item',
    props: ['movie'],
    methods: {
        handleClick() {
            eventBus.$emit('selected-movie', this.movie)
            
        }
    }
}
</script>

<style>

</style>