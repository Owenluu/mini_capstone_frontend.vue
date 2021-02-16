<template>
  <div class="home">
    <h1>All Blog Posts</h1>
    <div class="row row-cols-1 row-cols-md-2">
      <div class="col mb-4" v-for="post in posts" v-bind:key="post.id">
        <div class="card">
          <img v-bind:src="post.image" class="card-img-top" alt="..." />
          <div class="card-body">
            <h5 class="card-title">{{ post.title }}</h5>
            <p class="card-text">Body: {{ post.body }}</p>
            <a class="btn btn-primary" v-bind:href="`/posts.${post.id}`">More Info</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
img {
  width: 250px;
}
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      posts: [],
      title: "",
      body: "",
      image: "",
    };
  },
  created: function() {
    this.indexPosts();
  },
  methods: {
    indexPosts: function() {
      axios.get("/api/posts").then(response => {
        this.posts = response.data;
        console.log("All Post:", this.posts);
      });
    },
  },
};
</script>
