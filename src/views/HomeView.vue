<template>
  <div>
    Home
    <br />
    <input type="text" v-model="search" />
    <p>Search - {{ search }}</p>
    <div v-for="name in matchingSearch" :key="name">{{ name }}</div>
    <br /><br />
    
    
    <div v-if="error">{{ error }}</div>
    <div v-if="posts.length">
      <PostList :posts="posts" v-if="showPost" />
    </div>
    <div v-else>Loading...</div>
    <button @click="showPost = !showPost">Toggle Posts</button>
    <button @click="posts.pop()">delete posts</button>
  </div>
</template>

<script>
import PostList from "../components/PostList.vue";
import { ref, computed, watch, watchEffect } from "vue";
export default {
  name: "Home",
  components: {
    PostList,
  },
  setup() {
    const search = ref("");
    const showPost = ref(true);
    const names = ref([
      "aye aye",
      "mya mya",
      "hla hla",
      "aung aung",
      "kyaw kyaw",
    ]);
    const posts = ref([]);
    const error = ref(null);

    watch(search, () => {
      console.log("Watch function run");
    });

    watchEffect(() => {
      console.log("watchEffect function run", search.value);
    });

    const matchingSearch = computed(() => {
      return names.value.filter((name) => name.includes(search.value));
    });

    const load = async () => {
      try {
        let data = await fetch("http://localhost:3500/posts");
        if (!data.ok) {
          throw Error("no data available");
        }

        posts.value = await data.json();
      } catch (err) {
        error.value = err.message;
        console.log(error.value);
      }
    };

    load();

    return {
      names,
      search,
      matchingSearch,
      posts,
      showPost,
      error,
    };
  },
};
</script>

<style></style>
