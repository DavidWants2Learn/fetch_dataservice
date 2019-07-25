<template>
  <div>

  </div>
</template>

<script>
import { eventBus } from '~/plugins/eventBus.js'

export default {
  name: 'receiver',
  created() {
    eventBus.$on('jsonData', (json) => {
      this.combinedData = json;
    });
  },
  mounted() {
    eventBus.$on('jsonData', (json) => {
      this.combinedData = json;
      console.log(this.combinedData)
    });
  }
}
</script>

<style>
</style>