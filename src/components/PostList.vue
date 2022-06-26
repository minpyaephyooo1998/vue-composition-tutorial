<template>
  <div>
      <h2>Post List</h2>
      <div v-for="post in posts" :key="post">
          <SinglePost :post="post" />
      </div>
</div>
</template>

<script>
import { onMounted, onUnmounted, onUpdated } from '@vue/runtime-core'
import SinglePost from "./SinglePost.vue"
export default {
    name: 'PostList',
    components: {
        SinglePost
    },
    props: ['posts'],
    setup(props) {
        onMounted(() => console.log('component mounted'));
        onUnmounted(() => console.log('component unMounted'));
        onUpdated(() => console.log('component updated'))
    }
}
</script>

<style>

</style>