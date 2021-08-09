<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" @click="setSat" />
    <h1>{{ sat }}</h1>
    <HelloWorld msg="Click the logo to update the inset value" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data() {
    return {
      sat: undefined,
    };
  },
  methods: {
    setSat() {
      this.sat = getComputedStyle(document.body).getPropertyValue('--sat');
    },
  },
  mounted() {
    window.onload = this.setSat;
  },
};
</script>

<style lang="scss">
:root {
  --sat: env(safe-area-inset-top);
  --sar: env(safe-area-inset-right);
  --sab: env(safe-area-inset-bottom);
  --sal: env(safe-area-inset-left);
}

@supports (padding: max(0px)) {
  html,
  body,
  header,
  footer,
  #app {
    min-height: calc(100% + env(safe-area-inset-top));
    padding-top: min(0vmin, env(safe-area-inset-top));
  }
}

body {
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  background-color: #2c3e50;
  position: relative;
  top: calc(env(safe-area-inset-top) * -1);
  padding-top: 100px;
}
</style>
