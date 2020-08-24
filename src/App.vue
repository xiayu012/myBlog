<template>
  <div id="app">
    <!-- show-blogs></!-->
    <!-- single-blog></!-->
    <!-- add-blog></!-->
    <blog-header></blog-header>
    <router-view></router-view>
  </div>
</template>

<script>
import AddBlog from './components/AddBlog'
import SingleBlog from './components/SingleBlog'
import ShowBlogs from './components/ShowBlogs'
import BlogHeader from './components/BlogHeader'

export default {
  name: 'App',
  components: {
    AddBlog,SingleBlog,ShowBlogs,BlogHeader
  }
}
</script>

<style>

</style>
