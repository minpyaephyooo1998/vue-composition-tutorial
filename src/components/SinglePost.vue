<template>
  <div>
    <router-link :to="{ name: 'postDetail', params: {id: post.id } }">
      <h3>{{ post.title }}</h3>
    </router-link>

    <p>{{ snippet }}</p>
    <span v-for="tag in post.tags" :key="tag">#{{ tag }}</span>
  </div>
</template>

<script>
import { computed } from "vue";
export default {
  props: ["post"],
  setup(props) {
    console.log(props.post);
    const snippet = computed(() => {
      return props.post.body.substring(0, 100) + "...";
    });

    return {
      snippet,
    };
  },
};
</script>

<style></style>
