<template>
  <div id="add-blog">
    <h2>Add new blog</h2>
    <form v-if="!submitted">
      <label for="title">Title</label>
      <input type="text" required v-model.lazy="blog.title" />

      <label for="Content">Content</label>
      <textarea name="content" id="content" v-model.lazy="blog.content"></textarea>

      <div id="checkboxes">
        <label for="category1">Category1</label>
        <input type="checkbox" value="category1" v-model="blog.categories" />

        <label for="category2">Category2</label>
        <input type="checkbox" value="category2" v-model="blog.categories" />

        <label for="category3">Category3</label>
        <input type="checkbox" value="category3" v-model="blog.categories" />

        <label for="category4">Category4</label>
        <input type="checkbox" value="category4" v-model="blog.categories" />
      </div>

      <label for="author">Author</label>
      <select class="author" v-model="blog.author">
        <option v-for="author in authors" v-bind:key="author">{{author}}</option>
      </select>
      <div id="submit-button">
        <button @click.prevent="post" class="button button1">Add Blog</button>
      </div>
    </form>
    <div v-if="submitted">
      <h3>Thank you!</h3>
    </div>

    <div id="preview">
      <h3>Blog Preview</h3>
      <p>Title:{{blog.title}}</p>
      <p>Content:</p>
      <p>{{blog.content}}</p>
      <p>Categories</p>
      <ul>
        <li v-for="category in blog.categories" v-bind:key="category">{{category}}</li>
      </ul>
      <p>Written By: {{blog.author}}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blog: {
        title: "",
        content: "",
        categories: [],
        author: "",
      },
      authors: ["Rushan Tamrakar", "Rahul Krishna Kharel", "Kapil Shrestha"],
      submitted: false,
    };
  },

  methods: {
    post: function () {
      this.$http
        .post("https://vue-blog-app-bd0de.firebaseio.com/blogs.json", this.blog)
        .then(function (data) {
          console.log(data);
          this.submitted = true;
        });
    },
  },
};
</script>

<style scoped>
#add-blog * {
  box-sizing: border-box;
}

#add-blog {
  margin: 20px auto;
  max-width: 500px;
}

label {
  display: block;
  margin: 20px 0 10px;
}

input[type="text"],
textarea {
  display: block;
  width: 100%;
  padding: 8px;
}

#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}

h3 {
  margin-top: 10px;
}

#checkboxes input {
  display: inline-block;
  margin-right: 10px;
}

#checkboxes label {
  display: inline-block;
}

#submit-button {
  margin-top: 20px;
}

.button {
  background-color: #4caf50; /* Green */
  border: none;
  color: white;
  padding: 5px 15px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

.button1 {
  background-color: white;
  color: black;
  border: 2px solid #555555;
}

.author {
  width: 100%;
  height: 30px;
}
</style>