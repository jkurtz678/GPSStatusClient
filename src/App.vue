<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>One Step GPS: Active Devices</h1>
    <button @click="latestPoint">Get latest points</button>
    <DevicesContainer v-bind:devices="devices"/>
  </div>
</template>

<script>
import DevicesContainer from "./components/DevicesContainer.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    DevicesContainer
  },
  data() {
    return {
      devices: []
    };
  },
  methods: {
    latestPoint() {
      axios
        .get("http://localhost:8080/latest")
        .then(res => (this.devices = res.data.result_list))
        .catch(err => err);
    }
  }
};
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

button {
  font-size: 1.6em;
  background: #94fccd;
  border-radius: 10px;
}
</style>
