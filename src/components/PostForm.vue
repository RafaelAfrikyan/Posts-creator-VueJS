<template>
  <form class="form" @submit.prevent>
    <MyInput v-model="post.title" placeholder="Post Title" />
    <MyInput v-model="post.body" placeholder="Post Description" />
    <MyButton class="btn" @click="addPost">Add</MyButton>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: "",
        body: "",
      },
    };
  },

  methods: {
    addPost() {
      this.post.id = Date.now();
      this.post.likes = 0;
      this.$emit("create", this.post);
      this.post = {
        title: "",
        body: "",
        id: Date.now(),
      };
    },
  },
};
</script>

<style scoped>
.form {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 6px;
  flex-direction: column;
  width: 100%;
}
</style>
