<template>
  <div class="dialog" v-if="show" @click="hideDialog">
    <div @click.stop class="dialog__content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "MyDialog",
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    hideDialog() {
      this.$emit("update:show", false);
    },
  },
};
</script>

<style scoped>
.dialog {
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
  align-items: center;
  justify-content: center;
}
.dialog__content {
  margin: auto;
  padding: 0 24px;
  background: white;
  border-radius: 12px;
  min-width: 550px;
  min-height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
