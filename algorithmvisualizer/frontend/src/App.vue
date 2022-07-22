<template>
  <div id="app">

    <BubbleSort />
  </div>
</template>

<script>
import BubbleSort from './components/BubbleSort.vue'

export default {
  name: 'App',

  components: {
    BubbleSort: BubbleSort
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
