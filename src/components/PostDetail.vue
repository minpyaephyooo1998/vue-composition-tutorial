<template>
  <div>
      <h1>Post Detail</h1>
      <div v-if="error">{{error}}</div>
      <div v-if="post">
          <h3>{{ post.title }}</h3>
          <p>{{ post.body }}</p>
          <span>{{ tag }}</span>
      </div>
  </div>
</template>

<script>
import getPost from "../composables/getPost"
export default {
    name: 'PostDetail',
    props: ['id'],
    setup(props) {
        const { post, error, load } = getPost(props.id);
        
        load();

        return {
            post,
            error
        }
    }
}
</script>

<style>

</style>