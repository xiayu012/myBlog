<template>
  <div id="add-blog">
    <form v-if="!submitted">
    <h2>添加博客</h2>

    <label>博客标题</label>
    <input required v-model="blog.title" type="text">

    <label>博客内容</label>
    <textarea v-model="blog.content"></textarea>

    <div id="addBlog">
      <button v-on:click.prevent="post" ><span>添加博客</span></button>
    </div>
    </form>

<div v-if="submitted">
  <h3>添加博客成功！</h3>
</div>

    <hr>

    <div id="preview">
      <h3>博客预览：</h3>
      <p>博客标题：{{ blog.title }} </p>
      <p>博客内容：</p>  
      <p>{{ blog.content }}</p>
    </div>

  </div>
</template>

<script>
export default {
  name: 'add-blog',
  data () {
    return {
      blog:{
        title:"",
        content:"",
      },
      submitted:false
    }
  },
  methods:{
    post:function() {
      this.$http.post("https://blog-e1331.firebaseio.com/posts.json",this.blog)
        .then(function(data) {
          console.log(data);
          this.submitted = true;
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#add-blog *{
  box-sizing: border-box;
}
#add-blog {
  margin: 20px;
  max-width: 600px;
  padding: 20px;
}
label{
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],textarea{
  display: block;
  width: 100%;
  padding: 8px;
}
textarea{
  height: 200px;
}

#addBlog {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px;
}

button{
  display: block;
  margin: 10px 0;
  background: transparent;
  border: 0;
  padding: 14px;
  border-radius: 4px;
  font-size: 18px;
  cursor: pointer;
  position: relative;
  font-weight: bold;
}

button:before {
  transition: all 2,8s cubic-bezier(0.7, -0.5, 0.2, 2);
  content: '';
  width: 1%;
  height: 100%;
  background: #ff5964;
  position: absolute;
  top: 0;
  left: 0;
}

button span {
  mix-blend-mode: darken;
}
button:hover:before {
  background: #ff5964;
  width: 100%;
}
#preview{
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}
h3{
  margin-top: 10px;
}
</style>
