<template>
  <div id="blog">
    <h2>{{ heading }}</h2>
    <form v-if="!submitted">
      <div class="blog-header">
        <label>Title:</label>
        <input
          type="text"
          v-model.lazy="blogs.title"
          placeholder="Blog title..."
        />
        Content:
        <textarea
          v-model.lazy="blogs.content"
          placeholder="Write contents..."
        ></textarea>
        <div class="checkboxes">
          <p>Categories:</p>
          <label>VueJs</label>
          <input type="checkbox" value="VueJs" v-model="blogs.category" />
          <label>Wizard</label>
          <input type="checkbox" value="Wizard" v-model="blogs.category" />
          <label>Harry Potter</label>
          <input
            type="checkbox"
            value="Harry Potter"
            v-model="blogs.category"
          />
          <label>Cars</label>
          <input type="checkbox" value="Cars" v-model="blogs.category" />
        </div>
        <p>
          Authors:
          <select v-model="blogs.author">
            <option v-for="author in authors" v-bind:key="author">{{
              author
            }}</option>
          </select>
        </p>
        <button v-on:click.prevent="post">Add Blog</button>
      </div>
    </form>

    <div v-if="submitted">
      <h3>Thank you for Adding a blog</h3>
    </div>
    <div class="blog-review">
      <p v-show="center">Blog Review</p>
      <label>Title : {{ blogs.title }}</label>

      <br />
      <label>Content:</label>
      <p>{{ blogs.content }}</p>
      <p>category:</p>
      <ul>
        <li v-for="categor in blogs.category" v-bind:key="categor">
          {{ categor }}
        </li>
      </ul>
      <p>Author: {{ blogs.author }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blogs: {
        title: "",
        content: "",
        category: [],
        author: ""
      },
      authors: ["vivek", "ramakrishna", "kishan", "harish"],
      heading: "Add a New Blog Post",
      submitted: false
    };
  },
  methods: {
    post: function() {
      this.submitted = true;
      this.$http
        .post("https://jsonplaceholder.typicode.com/posts", {
          userId: 1,
          title: this.blogs.title,
          body: this.blogs.content
        })
        .then(function(data) {
          console.log(data);
          this.submitted = true;
        });
    }
  }
};
</script>

<style>
body {
  background: #ddd;
}
h2 {
  padding-top: 10px;
  margin-left: 130px;
}
#blog {
  margin: 0 auto;
  width: 530px;
  margin-top: 50px;
  min-height: 350px;
  background: #fff;
  border-radius: 10px;
  box-shadow: 5px 10px #9c9b9b;
  /* display: block; */
  padding-bottom: 20px;
}
#blog .blog-header {
  margin-left: 10px;
  box-sizing: border-box;
  width: 500px;
  border: 1px solid black;
  padding: 10px;
  min-height: 200px;
}
#blog .blog-header input {
  width: 450px;
  padding: 5px;
}

#blog .blog-header textarea {
  min-width: 470px;
  margin-top: 5px;
}

#blog .blog-review {
  /* margin-left: 10px;
  margin-top: 10px; */
  margin: 10px;
  box-sizing: border-box;
  width: 500px;
  border: 1px solid black;
  padding: 10px;
  min-height: 100px;
}
p {
  margin: 0px;
}
/* #blog .blog-review label {
  padding: 5px;
} */

.checkboxes input {
  display: inline-block;
}

.checkboxes label {
  display: inline-block;
}
</style>
