<template>
  <show-blogs></show-blogs>
</template>

<script>
import addBlog from "./components/addBlog.vue";
import showblogs from "./components/showblogs.vue";
export default {
  components: {
    "add-blog": addBlog,
    "show-blogs": showblogs
  },
  data() {
    return {};
  }
};
</script>

<style >
</style>
