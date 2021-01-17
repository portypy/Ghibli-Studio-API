<template >

  <li>
      <p>»Name: {{vehicle.name}}</p>
      <p>Class: {{vehicle.vehicle_class}}«</p>
  </li>

</template>

<script>
export default {
name: 'vehicles',
props: ['vehicle']
}
</script>

<style>

</style>