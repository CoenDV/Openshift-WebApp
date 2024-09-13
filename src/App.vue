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

    axios.post("https://accb-2001-1c04-4200-9500-e8a5-8873-9c6f-9ac.ngrok-free.app/v1/chat/completions",
      {
        "messages": [
          {
            "content": "You are a helpful assistant.",
            "role": "system"
          },
          {
            "content": "What is the capital of France?",
            "role": "user"
          }
        ]
      }
    )
      .then(response => {
        console.log(response.data);
        this.aiMsg = response.choices.message.content;
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
