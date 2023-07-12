<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "MyButton",
};
</script>

<style scoped>
.btn {
  border: 1px solid green;
  background-color: white;
  color: rgb(103, 103, 103);
  width: 124px;
  height: 44px;
  cursor: pointer;
}
</style>
