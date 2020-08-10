<template>
  <div>
    <app-header></app-header>
    <router-view></router-view>
  </div>
</template>

<script>
import addBlog from "./components/AddBlog";
import showBlogs from "./components/ShowBlogs";
import listBlogs from "./components/ListBlogs";
import header from "./components/Header";


export default {
  components: {
    "add-blog": addBlog,
    "show-blog": showBlogs,
    "list-blog": listBlogs,
    "app-header": header,

  },
};
</script>

<style>
body {
  margin: 0;
  font-family: Helvetica;
}
</style>
