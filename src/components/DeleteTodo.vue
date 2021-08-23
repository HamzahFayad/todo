<template>
  <div class="deleteIcon">
    <div @click="deleteTodo" class="delete-icon"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: ["todoItem"],
  methods: {
    deleteTodo() {
      this.$emit("delete", this.todoItem);
    },
  },
};
</script>

<style lang="scss">
.deleteIcon {
  cursor: pointer;
}
.delete-icon {
  background-image: url("../assets/images/icon-cross.svg");
  background-size: cover;
  background-repeat: no-repeat;
  height: 18px;
  width: 18px;
  position: relative;
}
</style>