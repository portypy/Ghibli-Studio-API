<template lang="html">
  <div>
      <ul>
          <locations v-for="location in locations" :location="location"></locations>
      </ul>
  </div>
</template>

<script>
import { eventBus } from '../main'
import Locations from './Locations.vue'
export default {
    name: 'extra-details',
    props: ['locations'],
    components: {'locations': Locations}
}
</script>

<style>

</style>