<template>
  <div  id="show-blogs" >
    <h1>博客总览</h1>
    <input type="text" v-model="search" placeholder="搜索">
    <div v-for="blog in filteredBlogs" :key="blog" class="single-blog">
      <router-link v-bind:to="'/blog/' + blog.id">
        <h2>{{ blog.title }}</h2>
      </router-link>
      <article>
        {{ blog.content | snippet }}
      </article>
    </div>
  </div>
</template>

<script>
export default {
  name: 'show-blogs',
  data() {
    return{
      blogs:[],
      search:""
    }
  },
  created() {
    this.$http.get('https://blog-e1331.firebaseio.com/posts.json')
    .then(function(data) {
      //console.log(data);
      //console.log(data.json());
      return data.json();
      })
    .then(function(data) {
      var blogsArr = [];
      for(let i in data) {
        //console.log(data[i]);
        data[i].id = i;
        blogsArr.push(data[i]);
      }
      this.blogs = blogsArr;
      //console.log(this.blogs);
    })
  },
  computed:{
    filteredBlogs:function(){
      return this.blogs.filter((blog) => {
        return blog.title.match(this.search);
      })
    }
  }
}
</script>

<style scoped>
#show-blogs {
  max-width: 600px;
  margin: 0 auto;
  background: #6677cc;
  padding: 20px;
}
.single-blog {
  background: #eee;
  box-sizing: border-box;
  padding: 20px;
  margin: 20px 0;
}
.single-blog a{
  text-decoration: none;
  color: crimson;
}
</style>