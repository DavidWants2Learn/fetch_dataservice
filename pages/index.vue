<template>
  <div class="container">
    <div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  components: {
  },
  asyncData() {
    const localurl = 'http://localhost:3000/';
    var releaseJSON = 'release.json';
    var responsetimeJSON = 'responsetime.json';
    var statusJSON = 'statusJSON';
    var transactionJSON = 'transactionJSON';
    const urls = [
      'http://localhost:3000/release.json',
      'http://localhost:3000/responsetime.json',
      'http://localhost:3000/status.json',
      'http://localhost:3000/transaction.json'
      // url+releaseJSON,
      // url+responsetimeJSON,
      // url+statusJSON,
      // url+transactionJSON
    ];
    
    Promise.all(urls.map(url =>
      fetch(url)
        .then(checkStatus)
        .then(parseJSON)
        .catch(error => console.log("Error fetching data", error))
    ))
    .then(function(response) {
      return response.json();
    }).then (function(myJson) {
      console.log(JSON.stringify(myJson));
    // }).catch(function(err) {
    });
  },
  mounted() {
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
