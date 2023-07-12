<template>
  <div class="post">
    <div class="post-content">
      <div><strong> Post title:</strong> {{ post.title }}</div>
      <div class="post-description">
        <strong> Post Description: </strong> {{ post.body }}
      </div>
      <div><strong>Likes: </strong>{{ post.likes }}</div>
      <MyButton @click="addLike(post.id)">Like</MyButton>
    </div>
    <MyButton @click="delPost(post.id)">Delete</MyButton>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addLike(id) {
      this.$emit("addLike", id);
    },
    delPost(id) {
      this.$emit("delPost", id);
    },
  },
};
</script>

<style scoped>
.post {
  padding: 14px;
  border: 1px solid green;
  margin-top: 14px;
  display: flex;
  align-items: center;
  justify-content: space-around;
  flex-direction: row;
}

.post-content {
  display: flex;
  gap: 12px;
  flex-direction: column;
  width: 80%;
}
</style>
