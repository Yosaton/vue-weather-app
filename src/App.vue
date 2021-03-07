<template>
<div>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <v-card raised>
    HelloWorld
  </v-card>
<v-form @submit.prevent="apiCall">
  <label for="fname">City:</label>
  <input type="text" v-model="city" id="fname" name="fname">
  <input
    type="submit"
    value="submit"
  >
</v-form>
  <div v-if="this.weather.main != undefined">
    <h1>{{ this.weather.main.temp}}</h1>
  </div>
</div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import {apiKey} from './ApiKey.js';


export default {
  name: 'App',
  data(){
    return{
      weather: {},
      city: '',
    }
  },
  components: {
    // HelloWorld
  },
  methods: {
    apiCall(){
      fetch(`http://api.openweathermap.org/data/2.5/weather?q=${this.city}&APPID=${apiKey}&units=imperial`)
        .then(res => res.json())
        .then(data => this.weather = data)
        .then(console.log(this.weather));
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
