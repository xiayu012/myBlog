<template>
  <div id="single-blog">
    <h1>{{blogs}}</h1>
  </div>
</template>

<script>
export default {
  name:"single-blog",
  data(){
    return{
      id:this.$route.params.id,
      blogs:{},
    }
  },
  created() {
    this.$http.get('https://blog-e1331.firebaseio.com/posts/' + this.id + '.json') 
    .then(function(data) {
      return data.json() ;
    })
    .then(function(data) {
      this.blogs = data.title;
    })
  }
}
</script>


<style scoped>
#single-blog{
  max-width: 960px;
  margin: 0 auto;
  padding: 20px;
  background: #eee;
  border: 1px dotted #aaa;
}
</style>