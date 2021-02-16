<template>
  <div class="signup">
    <form v-on:submit.prevent="createPost()">
      <h1>New Blog Posts</h1>
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
      title: "",
      body: "",
      image: "",
      errors: [],
    };
  },
  methods: {
    createPost: function() {
      var params = {
        title: this.title,
        body: this.body,
        image: this.image,
        // user_id: this.userID,
      };
      axios
        .post("/api/posts", params)
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
