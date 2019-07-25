<template>
  <div>

  </div>
</template>

<script>
import { eventBus } from '~/plugins/eventBus.js'

export default {
  name: 'receiver',
  // mounted() {
  //   //   this.combinedData
  //   eventBus.$on('combinedData', Data => {
  //     console.log("Hello World");
  //   });
  // },
  created() {
    eventBus.$on('jsonData', (json) => {
      this.combinedData = json;
    });
    // console.log(this.combinedData);
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