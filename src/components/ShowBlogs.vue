<template>
  <div id="show-blogs">
    <h1>All Blogs</h1>
    <input type="text" v-model="search" placeholder="Search blogs" />
    <div class="single-blog" v-for="(blog,index) in filteredBlogs" v-bind:key="index">
      <router-link v-bind:to="'/blog/'+blog.id">
        <h2 v-colourize>{{blog.title | toUppercase}}</h2>
      </router-link>
      <article>{{ blog.content | snippet }}</article>
    </div>
  </div>
</template>

<script>
import searchMixin from "../mixins/searchMixin";
export default {
  data() {
    return {
      blogs: [],
      search: "",
    };
  },
  methods: {},
  created() {
    this.$http
      .get("https://vue-blog-app-bd0de.firebaseio.com/blogs.json")
      .then(function (data) {
        return data.json();
      })
      .then(function (data) {
        var blogsArray = [];
        for (let key in data) {
          data[key].id = key;
          blogsArray.push(data[key]);
        }
        this.blogs = blogsArray;
      });
  },
  computed: {},
  filters: {
    toUppercase: function (value) {
      return value.toUpperCase();
    },

    snippet: function (value) {
      return value.slice(0, 100) + "...";
    },
  },
  directives: {
    colourize: {
      bind(el, binding, vnode) {
        el.style.color = "#" + Math.random().toString().slice(2, 8);
      },
    },
  },
  mixins: [searchMixin],
};
</script>

<style scoped>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}

.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee;
}

input[type="text"] {
  display: block;
  width: 100%;
  padding: 8px;
}
</style>