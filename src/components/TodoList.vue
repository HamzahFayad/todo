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
        <div class="delete">
          <DeleteTodo :todoItem="todo" @delete="onDelete" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DeleteTodo from "./DeleteTodo.vue";
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
  components: {
    DeleteTodo,
  },
  methods: {
    addTodo() {
      this.todolist.push({
        id: this.todolist.length + 1,
        name: this.inputText,
      });
      this.inputText = "";
      console.log(this.inputText);
    },
    onDelete(item) {
      console.log(item, "..");
      this.todolist.splice(item, 1);
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
    position: relative;
    color: #fff;
    margin: 8px auto;
    width: 400px;
    height: 50px;
    background: hsl(235, 24%, 19%);
    border-radius: 8px;
    font-size: 1rem;
    font-family: "Josefin Sans";
    //line-height: 40px;

    p {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      text-align: left;
      padding: 0 20px;
    }
    .delete {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      display: inline-block;
      padding: 0 160px;
    }
  }
}
@media only screen and(max-width: 400px) {
  .todo-add {
    .add-input {
      input {
        width: 300px;
      }
    }
  }
  .todos {
    .list {
      width: 300px;
      .delete {
        padding: 0 110px;
      }
    }
  }
}
</style>