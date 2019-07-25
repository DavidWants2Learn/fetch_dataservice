<template>
  <div>
  </div>
</template>

<script>
import { eventBus } from '~/plugins/eventBus.js'

export default {
  name: "status-panel",
  components: {
  },
  data() {
    return {
      jsonData: eventBus.$emit('test-event', this.combinedData)
    }
  },
  asyncData() {
    // 'http://localhost:3000/release.json',
    // 'http://localhost:3000/responsetime.json',
    // 'http://localhost:3000/status.json',
    // 'http://localhost:3000/transaction.json'
    
    // url+releaseJSON,
    // url+responsetimeJSON,
    // url+statusJSON,
    // url+transactionJSON
  },
  props: [
    'combinedData'
  ],
  methods: {
    switchName() {
      return this.myName;
    },
    emitData() {
      this.$emit("combinedData", this.combinedData);
    }
  },
  mounted() {
    const localurl = 'http://localhost:3000/';
    var releaseJSON = 'release.json';
    var responsetimeJSON = 'responsetime.json';
    var statusJSON = 'status.json';
    var transactionJSON = 'transaction.json';

    var releaseJSONRequest = 
    fetch(localurl+releaseJSON)
    .then(function(response) {
      return response.json()
    });

  var responseTimeJSONRequest = 
  fetch(localurl+responsetimeJSON)
    .then(function(response) {
      return response.json()
    });

  var statusJSONRequest = 
  fetch(localurl+statusJSON)
    .then(function(response) {
      return response.json()
    });

  var transactionJSONRequest = 
  fetch(localurl+transactionJSON)
    .then(function(response) {
      return response.json()
    });
  
  var combinedData = {
    releaseJSONRequest: {},
    responseTimeJSONRequest: {},
    statusJSONRequest: {},
    transactionJSONRequest: {}
    };
  Promise.all([
    releaseJSONRequest,
    responseTimeJSONRequest,
    statusJSONRequest,
    transactionJSONRequest])
    .then(function(data) {
      combinedData["releaseJSONRequest"] = data[0]["release"];
      combinedData["responseTimeJSONRequest"] = data[1]["metrics"];
      combinedData["statusJSONRequest"] = data[2];
      combinedData["statusJSONRequest"] = data[2]["environments"];
      combinedData["statusJSONRequest"] = data[2]["incidents"]
      combinedData["transactionJSONRequest"] = data[3]["metrics"];
      eventBus.$emit('jsonData', JSON.stringify(combinedData));
      return JSON.stringify(combinedData);
    });
    // console.log(combinedData)

  // this.$bus.$emit('test-event', combinedData);
  }
}
</script>

<style>

</style>