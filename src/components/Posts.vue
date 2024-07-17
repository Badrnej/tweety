<template>
  <!-- Posts -->
  <ul class="posts">
    <li v-for="post in posts" :key="post.id" class="flex gap-3">
      <img
        v-if="post.user.avatar_url"
        class="w-14 h-14 rounded-full ml-3"
        :src="require(`@/${post.user.avatar_url}`)"
        alt="User Avatar"
      />

      <div class="w-full h-full">
        <div class="flex gap-3 mb-2">
          <p>{{ post.user ? post.user.name : "Unknown User" }}</p>
          <p>@{{ post.user ? post.user.user_name : "unknown" }}</p>
          <p>. 5h</p>
        </div>

        <p class="w-[70%] mb-4">
          {{ post.content }}
        </p>
        <img
          v-if="post.image_url"
          :src="require(`@/${post.image_url}`)"
          alt="Post Image"
          class="w-[70%] rounded-3xl border border-[lightgray]"
        />
        <div class="w-[40%] post-icns flex justify-between p-5">
          <p @click="toggleLike(post)">
            <img
              :src="
                post.liked
                  ? require('../assets/icons/heartLiked.svg')
                  : require('../assets/icons/heart.svg')
              "
              alt="Heart Icon"
            />
            {{ formatNumber(post.likes_count) }}
          </p>
          <p>
            <img src="../assets/icons/comments.svg" alt="" />
            {{ formatNumber(post.comments_count) }}
          </p>
        </div>
      </div>
    </li>
  </ul>
</template>

<style>
body {
  color: rgb(57, 57, 54);
}

.post-icns p {
  display: flex;
  gap: 8px;
  cursor: pointer;
}

.posts li {
  padding-top: 12px;
  border-bottom: 1px solid rgb(46, 44, 44);
}
</style>

<script>
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  name: "PostsContainer",
  setup() {
    const posts = ref([]);

    async function fetchPosts() {
      try {
        const [postsResponse, usersResponse] = await Promise.all([
          axios.get("http://localhost:3000/Posts"),
          axios.get("http://localhost:3000/Users"),
        ]);

        const usersMap = usersResponse.data.reduce((acc, user) => {
          acc[user.id] = user;
          return acc;
        }, {});

        posts.value = postsResponse.data.map((post) => ({
          ...post,
          user: usersMap[post.user_id],
        }));
      } catch (error) {
        console.error("Error fetching posts:", error);
      }
    }

    async function toggleLike(post) {
      try {
        const updatedPost = {
          ...post,
          liked: !post.liked,
          likes_count: post.liked ? post.likes_count - 1 : post.likes_count + 1,
        };

        await axios.put(`http://localhost:3000/Posts/${post.id}`, updatedPost);

        const index = posts.value.findIndex((p) => p.id === post.id);
        if (index !== -1) {
          posts.value[index] = { ...updatedPost, user: post.user };
        }
      } catch (error) {
        console.error("Error toggling like:", error);
      }
    }

    function formatNumber(number) {
      if (number >= 1000000000) {
        return (number / 1000000000).toFixed(1) + "B";
      } else if (number >= 1000000) {
        return (number / 1000000).toFixed(1) + "M";
      } else if (number >= 1000) {
        return (number / 1000).toFixed(1) + "K";
      }
      return number;
    }

    onMounted(fetchPosts);

    return {
      posts,
      formatNumber,
      toggleLike,
    };
  },
};
</script>
