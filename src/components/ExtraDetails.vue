<template lang="html">
  <div>
      <ul>
          <locations v-for="location in locations" :location="location"></locations>
      </ul>
      <ul>
          <vehicles v-for="vehicle in vehicles" :vehicle="vehicle"></vehicles>
      </ul>
  </div>
</template>

<script>
import { eventBus } from '../main'
import Locations from './Locations.vue'
import Vehicles from './Vehicles'
export default {
    name: 'extra-details',
    props: ['locations', 'vehicles'],
    components: {
        'locations': Locations,
        'vehicles': Vehicles
    }
}
</script>

<style lang="css" scoped>
ul {
    list-style-type: none;
    padding: 0%;
  }
</style>