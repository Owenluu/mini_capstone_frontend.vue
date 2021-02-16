<template>
  <div class="post-edit">
    <form v-on:submit.prevent="createPost()">
      <h1>Edit Blog Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <br />
        <input type="text" class="form-control" v-model="title" />
      </div>
      <div class="form-group">
        <label>Body:</label>
        <br />
        <!-- <input type="text" class="form-control" v-model="body" /> -->
        <textarea Class="form-control" v-model="body"></textarea>
      </div>
      <div class="form-group">
        <label>Image:</label>
        <br />
        <input type="text" class="form-control" v-model="image" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      post: {},
      title: "",
      body: "",
      image: "",
      errors: [],
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
        this.title = this.post.title;
        this.body = this.post.body;
        this.image = this.post.image;
      });
    },
    updatePost: function() {
      var params = {
        title: this.title,
        body: this.body,
        image: this.image,
      };
      axios
        .patch("/api/posts/" + this.$route.params.id, params)
        .then(response => {
          console.log(response);
          this.$router.push("/posts");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
