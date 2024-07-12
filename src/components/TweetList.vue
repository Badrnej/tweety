<template>
    <div>
      <TweetItem
        v-for="tweet in tweets"
        :key="tweet.id"
        :tweet="tweet"
      />
    </div>
  </template>
  
  <script>
  import TweetItem from './TweetItem.vue';
  
  export default {
    name: 'TweetList',
    components: { TweetItem },
    data() {
      return {
        tweets: []
      }
    },
    created() {
      fetch('http://localhost:3000/tweets')
        .then(response => response.json())
        .then(data => this.tweets = data);
    }
  }
  </script>
  