<template>
  <div class="container mx-auto">
    <Navbar />
    <div class="flex space-x-4">
      <TweetList />
      <UserSuggestions />
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import TweetList from './components/TweetList.vue';
import UserSuggestions from './components/UserSuggestions.vue';

export default {
  name: 'App',
  components: { Navbar, TweetList, UserSuggestions }
}
</script>


