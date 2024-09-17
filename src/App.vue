<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App" />
  <p>{{ msg }}</p>
  <p>{{ aiMsg }}</p>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  mounted() {
    axios.get("https://openshift-test-git-coen-de-vries-dev.apps.sandbox-m4.g2pi.p1.openshiftapps.com/api")
      .then(response => {
        this.msg = response.data;
      })
      .catch(error => {
        console.log(error);
      });

    axios.post("https://saved-ferret-rapid.ngrok-free.app/generate",
      {
        "prompt": "what is the capital of france?"
      }
    )
      .then(response => {
        console.log(response.data);
        this.aiMsg = response.data.choices[0].message.content;
      })
      .catch(error => {
        console.log(error);
      });

  },
  data() {
    return {
      msg: '',
      aiMsg: ''
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
