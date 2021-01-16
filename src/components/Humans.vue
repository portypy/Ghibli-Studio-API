<template>
  <li>
     {{human.name}}  Age: {{human.age}}
  </li>
</template>

<script>
export default {
name: 'humans',
props: ['human']
}
</script>

<style>

</style>