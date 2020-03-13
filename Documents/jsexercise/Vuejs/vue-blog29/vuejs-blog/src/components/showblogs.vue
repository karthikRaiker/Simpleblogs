<template>
  <div v-theme:column="'narrow'" id="show-blogs">
    <h2>Show Blog Articles</h2>
    <div v-for="blog in blogs" v-bind:key="blog.id" class="single-blog">
      <h3 v-rainbow>{{blog.title}}</h3>
      <article>{{blog.body}}</article>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blogs: []
    };
  },
  created() {
    this.$http
      .get("https://jsonplaceholder.typicode.com/posts")
      .then(function(data) {
        this.blogs = data.body.splice(0, 10);
        console.log(this.blogs);
      });
  }
};
</script>

<style >
#show-blogs {
  max-width: 900px;
  margin: 20px auto;
}

.single-blog {
  max-width: 850px;
  background-color: #eee;
  padding: 1px 10px 10px 10px;
  margin: 10px;
}
</style>
