<template lang="html">
  <div>
      <ul>
          <list-item class="list-item" v-for="movie in movies" :movie="movie"></list-item>
      </ul>
  </div>
</template>

<script>
import ListItem from './ListItem.vue'
export default {
    name: "movies-list",
    props: ["movies"],
    components:{'list-item': ListItem}
}
</script>

<style lang="css" scoped>
ul {
    list-style-type: none;
    padding: 0%;
  }
.list-item:hover {
    color: whitesmoke;
}
</style>