<template>
  <!-- Trending Bar -->
  <aside class="w-[25vw] h-auto border-[1px] border-[lightgray] rounded-[20px]">
    <ul class="trending">
      <li>
        <h1 class="text-xl font-bold">Trending for you</h1>
      </li>
      <li v-for="trend in trends" :key="trend.id">
        <p>Trending in {{ trend.location }}</p>
        <h3>{{ trend.hashtag }}</h3>
        <p>{{ formatNumber(trend.Tweets_count) }} Tweets</p>
      </li>
    </ul>
  </aside>
</template>

<style>
.trending li {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  color: rgb(0, 0, 0);
  padding: 12px 30px;
  border-bottom: 1px solid lightgray;
}

.trending li:last-child {
  border-bottom: none;
}

.trending li p {
  color: gray;
  font-size: 13px;
}
</style>

<script>
import { ref, onMounted } from "vue";
import axios from "axios";

export default {
  name: "TrendingBar",
  setup() {
    const trends = ref([]);

    async function fetchTrends() {
      try {
        const response = await axios.get("http://localhost:3000/Trends");
        trends.value = response.data;
      } catch (error) {
        console.error("Error fetching trends:", error);
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

    onMounted(fetchTrends);

    return {
      trends,
      formatNumber,
    };
  },
};
</script>
