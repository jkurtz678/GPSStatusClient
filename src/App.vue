<template>
  <div id="app">
    <img alt="One Step GPS logo" src="./assets/onestepgps.png" />
    <h1>My Active Devices:</h1>
    <div class="control-panel">
      <button class="updateBtn" @click="handleClick">Latest Points</button>
      <label class="checkbox-container">
        <input type="checkbox" ref="autoUpdateChecked" />auto update (5s)
      </label>
      <div v-if="updateInterval != null">
        Auto updating in {{ this.updateTime
        }}<button class="cancelBtn" @click="cancelAutoUpdate">Cancel</button>
      </div>
    </div>
    <DevicesContainer
      v-bind:devices="devices"
      v-bind:waitingForResponse="waitingForResponse"
    />
    <footer>Developed by Jackson Kurtz</footer>
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
      devices: [],
      waitingForResponse: false,
      updateInterval: null,
      updateTime: 5
    };
  },
  methods: {
    latestPoints() {
      this.waitingForResponse = true;
      axios
        .get("http://localhost:8080/latest")
        .then(res => {
          this.waitingForResponse = false;
          this.devices = res.data.result_list;
        })
        .catch(err => err);
    },
    clockTick() {
      this.updateTime--;
      if (this.updateTime === 0) {
        this.latestPoints();
        this.updateTime = 5;
      }
    },
    handleClick() {
      this.latestPoints();
      if (this.$refs.autoUpdateChecked.checked && this.updateInterval == null) {
        this.updateInterval = setInterval(() => {
          this.clockTick();
        }, 1000);
      }
    },
    cancelAutoUpdate() {
      clearInterval(this.updateInterval);
      this.updateInterval = null;
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
  color: #094079;
  margin-top: 60px;
}

button {
  font-size: 1.4em;
  /*background: #8ccdff;*/
  background: #54b2f9;
  color: #094079;
  border-radius: 10px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

.updateBtn {
  margin-right: 50px;
  margin-bottom: 30px;
}

.cancelBtn {
  margin-left: 50px;
  font-size: 1em;
}

button:hover {
  background: #93d0ff;
}

input {
  margin-right: 7px;
}

.control-panel {
  margin-bottom: 10px;
}
footer {
  font-size: 0.8em;
  margin: 30px;
  flex-shrink: 0;
}
</style>
