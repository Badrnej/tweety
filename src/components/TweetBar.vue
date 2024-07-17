<template>
  <!-- Tweet Bar -->
  <nav class="p-4 border-[1px] border-[lightgray]">
    <div>
      <form @submit.prevent="submitPost">
        <div class="flex my-3">
          <img
            class="w-10 h-10 rounded-full"
            src="../assets/Profile.png"
            alt=""
          />
          <div class="w-[70%]">
            <input
              v-model="postContent"
              type="text"
              placeholder="What's happening?"
              class="w-full h-10 ml-5 pl-4 border-[1px] border-[lightgray] rounded-full"
            />
          </div>

          <button
            type="submit"
            class="w-28 ml-10 p-2 bg-blue-500 text-white rounded-full"
          >
            Tweet
          </button>
        </div>
      </form>
    </div>
  </nav>
</template>

<style>
nav {
  border-left: none;
  border-right: none;
  height: fit-content;
}
</style>

<script>
import { ref } from "vue";
import axios from "axios";

export default {
  name: "TweetBar",
  setup() {
    const postContent = ref("");

    async function submitPost() {
      if (!postContent.value) {
        alert("Please enter some content.");
        return;
      }

      try {
        const response = await axios.get("http://localhost:3000/Posts");
        const posts = response.data;
        const lastId =
          posts.length > 0 ? parseInt(posts[posts.length - 1].id) : 0;
        const newId = lastId + 1;

        const postData = {
          id: newId.toString(),
          content: postContent.value,
          liked: false,
          likes_count: 0,
          comments_count: 0,
          created_at: new Date().toISOString(),
          user_id: "1",
        };

        await axios.post("http://localhost:3000/Posts", postData);

        postContent.value = "";
      } catch (error) {
        console.error("Error submitting post:", error);
        alert("Post submission failed.");
      }
    }

    return {
      postContent,
      submitPost,
    };
  },
};
</script>
