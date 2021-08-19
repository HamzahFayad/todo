<template>
  <div id="todolist">
    <div class="todo-add">
      <div class="add-input">
        <span></span>
        <input
          type="text"
          placeholder="Create a new todo..."
          v-model="inputText"
          @keyup.enter="addTodo()"
        />
      </div>
    </div>
    <div class="todos">
      <div class="list" v-for="todo in todolist" :key="todo.id">
        <p>{{ todo.name }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputText: "",
      todolist: [
        {
          id: 1,
          name: "Homework",
        },
        {
          id: 2,
          name: "Training",
        },
      ],
    };
  },
  components: {},
  methods: {
    addTodo() {
      this.todolist.push({
        id: todolist.length + 1,
        name: this.inputText,
      });
      console.log(this.inputText);
    },
  },
};
</script>


<style lang="scss">
#todolist {
  position: relative;
  height: 100vh;
  background: hsl(235, 21%, 11%);
}
.todo-add {
  position: absolute;
  top: -10%; /** ? **/
  left: 50%;
  transform: translate(-50%, -50%);
  .add-input {
    position: relative;
    input {
      width: 400px;
      height: 50px;
      background: hsl(235, 24%, 19%);
      outline: none;
      border: none;
      color: #fff;
      padding: 0 50px;
      border-radius: 8px;
      font-size: 0.85rem;
      font-family: "Josefin Sans";
      &::placeholder {
        color: #fff;
        opacity: 0.6;
      }
    }
    span {
      position: absolute;
      top: 50%;
      transform: translate(0, -50%);
      color: #fff;
      margin: 0 10px;
      width: 25px;
      height: 25px;
      border-radius: 50%;
      border: 2px solid hsla(234, 39%, 85%, 0.479);
    }
  }
}
.todos {
  margin-top: 25px;

  .list {
    color: #fff;
    margin: 8px auto;
    padding: 8px 0;
    width: 400px;
    height: 50px;
    background: hsl(235, 24%, 19%);
    outline: none;
    border: none;
    color: #fff;
    border-radius: 8px;
    font-size: 0.85rem;
    font-family: "Josefin Sans";
    line-height: 40px;
  }
}
</style>