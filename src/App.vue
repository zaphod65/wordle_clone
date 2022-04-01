<template>
  <GameContainer/>
</template>

<script>
import GameContainer from './components/GameContainer';

export default {
  name: 'App',
  components: {
    GameContainer,
  }
}
</script>

<style>
body {
  background-color: #121213;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
