<template lang="html">
  <div>
      <ul>
          <locations v-for="location in locations" :location="location"></locations>
          <locations></locations>
      </ul>
  </div>
</template>

<script>
import { eventBus } from '../main'
import Locations from './Locations.vue'
export default {
    name: 'extra-details',
    props: ['locations'],
    components: {'locations': Locations},
    // mounted(){
    //     eventBus.$on('locations', (locations) =>{
    //         this.locations = locations;
    //     })
    // }
}
</script>

<style>

</style>