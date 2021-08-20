<template>
  <div class="deleteIcon">
    <img @click="deleteTodo" src="../assets/images/icon-cross.svg" alt="" />
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
</style>