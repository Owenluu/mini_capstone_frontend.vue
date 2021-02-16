<template>
  <div>
    <h2>{{ post.title }}</h2>
    <p>{{ post.body }}</p>
    <a v-bind:href="`/posts/${post.id}/edit`">Edit This Post</a>
    <br />
    <a href="/posts">Back to all Posts</a>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      post: {},
    };
  },
  created: function() {
    this.showPost();
  },
  methods: {
    showPost: function() {
      axios.get("/api/posts/" + this.$route.params.id).then(response => {
        console.log(response.data);
        this.post = response.data;
      });
    },
  },
};
</script>
