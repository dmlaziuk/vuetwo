<template>
  <div id="app">
   <!-- <p>{{ message }}</p> -->
    <notebook/>
  </div>
</template>

<script>
import Notebook from './notebook.vue'

export default {
  data: function () {
    return {
      message: "Hello Vue!"
    }
  },
  components: { Notebook }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>
