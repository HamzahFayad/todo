<template>
  <div>
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
p {
  color: #fff;
}
</style>