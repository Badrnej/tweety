<template>
  <SideBar />
  <div class="flex">
    <main class="w-[51vw] ml-[20vw] border-[1px] border-[lightgray]">
      <h2 class="h-10 ml-5 text-xl font-bold text-white">Home</h2>
      <TweetBar />
      <PostsContainer />
    </main>
    <div>
      <SearchField />
      <TrendingBar />
    </div>
  </div>
</template>

<style>
body {
  background-color: black;
}

main {
  border-top: none;
  margin-right: 21px;
}
</style>

<script>
import "../src/style.css";
import SideBar from "./components/SideBar.vue";
import TrendingBar from "./components/Trending.vue";
import SearchField from "./components/SearchField.vue";
import TweetBar from "./components/TweetBar.vue";
import PostsContainer from "./components/Posts.vue";

export default {
  name: "App",
  components: {
    SideBar,
    TrendingBar,
    SearchField,
    TweetBar,
    PostsContainer,
  },
};
</script>
