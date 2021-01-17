<template lang="html">
  <div>
      <img src="../assets/fly.gif" height="150" id="fly">
      <ul>
          <locations v-for="location in locations" :location="location"></locations>
          <vehicles v-for="vehicle in vehicles" :vehicle="vehicle"></vehicles>
          <humans v-for="human in humans" :human="human"></humans>
      </ul>
  </div>
</template>

<script>
import { eventBus } from '../main'
import Locations from './Locations.vue'
import Vehicles from './Vehicles'
import Humans from './Humans'
export default {
    name: 'extra-details',
    props: ['locations', 'vehicles','humans'],
    components: {
        'locations': Locations,
        'vehicles': Vehicles,
        'humans': Humans
    }
}
</script>

<style lang="css" scoped>
ul {
    list-style-type: none;
    padding: 0%;
  }
  #fly{
  top: 10px;
  border: 3px solid green;
}
</style>