<template>
  <div id="app">
    <FreeCall/>
  </div>
</template>

<script>
import FreeCall from './pages/FreeCall';

export default {
  name: 'App',
  components: {
    FreeCall,
  },
};
</script>

<style lang="scss">
#app {
  /* font-family: 'Avenir', Helvetica, Arial, sans-serif; */
  font-family: 'Press Start 2P', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

  height: 100%;
}
</style>
