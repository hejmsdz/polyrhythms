<template>
  <div id="app">
    <Clock :size="400" :subdivisions="[x, y]" :active="[ax, ay]" />
    
    <div>
      <input type="number" min="1" max="16" v-model="x" :readonly="active" />
      :
      <input type="number" min="1" max="16" v-model="y" :readonly="active" />
    </div>
    <div>
      <button @click="start" v-if="!active">Start</button>
      <button @click="stop" v-if="active">Stop</button>
    </div>
  </div>
</template>

<script>
import Clock from './components/Clock.vue'

export default {
  name: 'app',
  components: {
    Clock
  },
  data: function() {
    return { x: 2, y: 3, ax: 0, ay: 0, active: false, xIntvl: null, yIntvl: null };
  },
  methods: {
    reset: function() {
      this.ax = 0;
      this.ay = 0;
    },
    start: function() {
      this.reset();
      const measure = 2000;
      this.xIntvl = setInterval(() => {
        this.ax++;
        this.ax %= this.x;
      }, measure / this.x);

      this.yIntvl = setInterval(() => {
        this.ay++;
        this.ay %= this.y;
      }, measure / this.y);

      this.active = true;
    },
    stop: function() {
      this.reset();
      clearInterval(this.xIntvl);
      clearInterval(this.yIntvl);
      this.active = false;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
