<template>
  <div id="jokes">
    <h3>{{title}}</h3>
    <DisplayJoke />
  </div>
</template>

<script>
import DisplayJoke from './components/DisplayJoke.vue';

export default {
  name: 'App',
  data: function() { 
    return {
      title: 'Jokes app made with VueJS and W3CSS',
    }
  },
  components: {
    DisplayJoke
  }
}
</script>

<style>
#jokes {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
