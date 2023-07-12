<template>
  <div>
    <h2>Post something</h2>
    <MyButton style="margin-bottom: 16px" @click="openDialog"
      >Add new post</MyButton
    >
    <MyInput v-model="searchQuery" placeholder="search" />
    <MyDialog v-model:show="dialogVisible">
      <PostForm @create="addPost" />
    </MyDialog>
    <PostList
      v-if="!this.isPostLoading"
      :posts="sortedSearchedPosts"
      @delPost="delPost"
      @addLike="addLike"
    />
    <h2 v-else>Loading...</h2>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import MyDialog from "./components/UI/MyDialog.vue";
import MyButton from "./components/UI/MyButton.vue";
import axios from "axios";
export default {
  components: {
    PostForm,
    PostList,
    MyDialog,
    MyButton,
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostLoading: false,
      searchQuery: "",
      page: 1,
    };
  },
  methods: {
    openDialog() {
      this.dialogVisible = true;
    },
    addPost(newPost) {
      if (newPost.title && newPost.body) {
        this.posts.unshift(newPost);
      }
      this.dialogVisible = false;
    },
    addLike(id) {
      this.posts.forEach((post) => {
        if (post.id === id) {
          post.likes += 1;
        }
      });
    },
    delPost(id) {
      this.posts = this.posts.filter((post) => post.id !== id);
    },
    async fetchPost() {
      this.isPostLoading = true;
      try {
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",
          {
            params: {
              _page: this.page,
              _limit: this.limit,
            },
          }
        );

        // some code should be transferred in other functions
        const data = response.data.map((post) => {
          const mutatedPost = { ...post };
          mutatedPost.likes = 0;
          return mutatedPost;
        });
        this.posts = this.posts.concat(data);
        this.isPostLoading = false;
      } catch (e) {
        alert("error");
      }
    },
  },
  computed: {
    sortedSearchedPosts() {
      return this.posts.filter((post) => post.title.includes(this.searchQuery));
    },
  },
  beforeMount() {
    this.fetchPost();
  },
};
</script>

<style>
#app {
  margin: 100px;
  padding: 0;
  box-sizing: border-box;
}
</style>
