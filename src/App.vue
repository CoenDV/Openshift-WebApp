<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <p>{{ msg }}</p>

  <h1>Ask a question: </h1>
  <input type="text" v-model="question" />
  <button @click="askQuestion">Ask</button>
  <h1>AI response:</h1>
  <p>{{ aiMsg }}</p>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  components: {
    
  },
  mounted() {
    axios.get("https://openshift-test-git-coen-de-vries-dev.apps.sandbox-m4.g2pi.p1.openshiftapps.com/api")
      .then(response => {
        this.msg = response.data;
      })
      .catch(error => {
        console.log(error);
      });
  },
  data() {
    return {
      msg: '',
      aiMsg: '',
      question: ''
    }
  },
  methods: {
    askQuestion() {
      axios.post("https://saved-ferret-rapid.ngrok-free.app/generate/",
        {
          "prompt": this.question
        }
      )
        .then(response => {
          console.log(response.data);
          this.aiMsg = response.data.response[0].message.content;
        })
        .catch(error => {
          console.log(error);
        });
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
