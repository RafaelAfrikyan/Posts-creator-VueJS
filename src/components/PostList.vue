<template>
  <div v-if="posts.length > 0">
    <transition-group name="post-list">
      <PostItem
        v-for="post in posts"
        :key="post.id"
        :post="post"
        @delPost="delPost"
        @addLike="addLike"
      />
    </transition-group>
  </div>
  <h2 v-else>There is no any post</h2>
</template>

<script>
import PostItem from "./PostItem.vue";
export default {
  components: {
    PostItem,
  },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
  methods: {
    delPost(id) {
      this.$emit("delPost", id);
    },
    addLike(id) {
      this.$emit("addLike", id);
    },
  },
};
</script>

<style scoped>
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.3s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
