<template>
  <div class="">
    <Header />
    <Boxxy />
  </div>
</template>

<script>
import Boxxy from './components/Boxxy.vue';
import Header from './components/Header.vue';

export default {
  name: 'App',
  components: {
    Boxxy,
    Header,
  },
};
</script>

<style lang="scss">
html,
body {
  background: #e9e3d9;
  padding: 0;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
