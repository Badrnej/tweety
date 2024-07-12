<template>
    <div class="border-b p-4">
      <h2 class="font-bold">{{ tweet.user }}</h2>
      <p>{{ tweet.content }}</p>
      <div class="flex space-x-2">
        <button @click="likeTweet">👍 {{ tweet.likes }}</button>
        <button @click="retweet">🔁 {{ tweet.retweets }}</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'TweetItem',
    props: ['tweet'],
    methods: {
      likeTweet() {
        // Logique de like ici
      },
      retweet() {
        // Logique de retweet ici
      }
    }
  }
  </script>
  