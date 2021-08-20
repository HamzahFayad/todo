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
        <!-- <div class="check" @click="doneTodo()">
          <img src="../assets/images/icon-check.svg" alt="" />
        </div>-->
        <p @click="todo.done = !todo.done" :class="{ completed: todo.done }">
          {{ todo.name }}
        </p>
        <div class="delete">
          <DeleteTodo :todoItem="todo" @delete="onDelete" />
        </div>
      </div>
      <div class="subInfos">
        <p>{{ todosLeft }} item<span v-show="todosLeft !== 1">s</span> left</p>
        <p>All</p>
        <p>Active</p>
        <p>Clear completed</p>
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
          done: false,
        },
        {
          id: 2,
          name: "Training",
          done: true,
        },
      ],
    };
  },
  components: {
    DeleteTodo,
  },
  computed: {
    todosLeft() {
      return this.todolist.filter((todo) => todo.done === false).length;
    },
  },
  methods: {
    addTodo() {
      this.todolist.push({
        id: this.todolist.length + 1,
        name: this.inputText,
        done: false,
      });
      this.inputText = "";
      console.log(this.inputText);
    },
    onDelete(item) {
      console.log(item, "...");
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
    margin: 0 auto;
    width: 400px;
    height: 50px;
    background: hsl(235, 24%, 19%);
    border-bottom: 1px solid rgba(255, 255, 255, 0.164);
    //border-radius: 8px;
    //border-bottom-left-radius: 0;
    //border-bottom-right-radius: 0;
    font-size: 1rem;
    font-family: "Josefin Sans";
    //line-height: 40px;
    p {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      text-align: left;
      padding: 0 50px;
      cursor: pointer;
    }
    .delete {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      display: inline-block;
      padding: 0 160px;
    }
  }
  .list:nth-child(1) {
    border-top-left-radius: 8px;
    border-top-right-radius: 8px;
  }
  .subInfos {
    position: relative;
    color: rgb(177, 177, 177);
    margin: 0 auto;
    width: 400px;
    height: 60px;
    background: hsl(235, 24%, 19%);
    border-bottom-left-radius: 8px;
    border-bottom-right-radius: 8px;
    font-size: 0.85rem;
    font-family: "Josefin Sans";
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-around;
    p {
      transform: translateY(65%);
    }
  }
  .completed {
    text-decoration: line-through;
    color: rgba(255, 255, 255, 0.425);
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