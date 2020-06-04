<template>
  <div id="test-bell">
    <Recipe />
  </div>
</template>

<script>
import Recipe from './components/Recipe.vue'

export default {
  name: 'App',
  components: {
    Recipe
  }
}
</script>

<style lang="scss">

  @import '../node_modules/milligram/dist/milligram.css';

</style>
