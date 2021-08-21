<template>
  <div id="header">
    <div class="head">
      <div class="xdx">
        <h1>Todo</h1>
        <!--<img src="../assets/images/icon-sun.svg" alt="" />-->
      </div>
    </div>
    <div class="todo">
      <TodoList />
    </div>
  </div>
</template>

<script>
import TodoList from "./TodoList.vue";
export default {
  name: "Header",
  components: {
    TodoList,
  },
};
</script>

<style lang="scss" scoped>
#header {
  position: relative;
}
.head {
  background-image: url("../assets/images/bg-desktop-dark.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  height: 250px;
  width: 100vw;
  position: relative;
  .xdx {
    padding: 100px 0;
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-around;
    align-items: center;

    h1 {
      color: rgb(255, 255, 255);
      font-weight: 400;
      text-transform: uppercase;
      letter-spacing: 6px;
      margin-top: 6px;
    }
    img {
      cursor: pointer;
    }
  }
}
/*.todo {
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translate(-50%, -50%);
}*/
</style>