<template>
  <div class="w3-container">
      <button class="w3-button w3-deep-orange w3-hover-orange" @click="getRandomJoke">Get a Joke</button>
      <hr />
      <div class="loader w3-spin" v-if="isFetching"></div>
      <div class="w3-panel w3-animate-zoom w3-deep-orange w3-large" v-else>
          <h3 v-if="joke">{{joke}}</h3>
          <p v-if="upvotes || downvotes">
              <button class="w3-btn w3-circle w3-hover-teal" @click="upvote">&#8657;</button> {{upvotes}}
              <button class="w3-btn w3-circle w3-hover-red" @click="downvote">&#8659;</button>{{downvotes}}
          </p>
      </div>
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: 'DisplayMessage',
  data: function() {
      return {
          joke: null,
          upvotes: null,
          downvotes: null,
          jokeId: null,
          isFetching: false
      }
  },
  methods: {
    getRandomJoke: function() {
        this.isFetching = true;
        axios.get('https://joke3.p.rapidapi.com/v1/joke', {
          "method": "GET",
          "headers": {
            "x-rapidapi-host": "joke3.p.rapidapi.com",
            "x-rapidapi-key": "f13d988d3fmshe40bacb14ff109ap1fa783jsn18e3b85e9e19"
          }
        })
        .then(res => {
            this.isFetching = false;
            this.joke = res.data.content,
            this.jokeId = res.data.id,
            this.upvotes = res.data.upvotes,
            this.downvotes = res.data.downvotes
        });
    },
    upvote: function() {
        this.upvotes = this.upvotes + 1;
    },
    downvote: function() {
        this.downvotes = this.downvotes + 1;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.w3-container, .w3-panel {
    padding: 0 16px;
}

button:focus {
    outline: none;
}

.loader {
    border: 16px solid #f3f3f3;
    border-radius: 50%;
    border-top: 16px solid #ff5722;
    width: 120px;
    height: 120px;
    margin: 0 auto;
}

</style>
