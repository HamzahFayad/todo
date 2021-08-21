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
      <draggable
        v-model="todolist"
        group="todos"
        @start="drag = true"
        @end="drag = false"
      >
        <div
          class="list"
          v-for="todo in todolist"
          :key="todo.id + '-' + todo.name"
        >
          <!-- <div class="check" @click="doneTodo()">
          <img src="../assets/images/icon-check.svg" alt="" />
        </div>-->
          <input
            @change="todo.done = !todo.done"
            :checked="todo.done"
            class="checkComplete"
            type="checkbox"
          />
          <p :class="{ completed: todo.done }">
            {{ todo.name }}
          </p>
          <div class="delete">
            <DeleteTodo :todoItem="todo" @delete="onDelete" />
          </div>
        </div>
      </draggable>
      <div class="subInfos">
        <p style="padding-right: 25px">
          {{ todosLeft }} item<span v-show="todosLeft !== 1">s</span> left
        </p>
        <!--<p>All</p>
        <p>Active</p>
        <p>Completed</p>-->
        <p
          @click="clearCompleted()"
          style="padding-left: 25px; cursor: pointer"
        >
          Clear completed
        </p>
      </div>
    </div>
    <p class="info">Drag and drop to reorder list</p>
  </div>
</template>

<script>
import DeleteTodo from "./DeleteTodo.vue";
import draggable from "vuedraggable";
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
      //allTodos: "all",
    };
  },
  /*filters: {
    activeTodos: (todos) => {
      return todos.filter((todo) => todo.done === false);
    },
    completedTodos: (todos) => {
      return todos.filter((todo) => todo.done === true);
    },
  },*/
  components: {
    DeleteTodo,
    draggable,
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
    },
    onDelete(item) {
      this.todolist.splice(this.todolist.indexOf(item), 1);
    },
    clearCompleted() {
      let completed = this.todolist.filter((todo) => todo.done === true);
      completed.forEach((elem) => {
        let i = this.todolist.indexOf(elem);
        this.todolist.splice(i, 1);
      });
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
      border-radius: 4px;
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
input[type="checkbox"] {
  filter: invert(100%) hue-rotate(-150deg) brightness(0.85);
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
    box-shadow: 2px 4px 6px black;
    border-bottom: 1px solid rgba(255, 255, 255, 0.164);
    font-size: 1rem;
    font-family: "Josefin Sans";
    cursor: pointer;
    p {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      margin: 0 50px;
      cursor: pointer;
    }
    .checkComplete {
      position: absolute;
      top: 50%;
      transform: translate(-1400%, -50%);
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
  .list:nth-child(1) {
    border-top-left-radius: 4px;
    border-top-right-radius: 4px;
  }
  .subInfos {
    position: relative;
    color: rgb(177, 177, 177);
    margin: 0 auto;
    width: 400px;
    height: 60px;
    background: hsl(235, 24%, 19%);
    border-bottom-left-radius: 4px;
    border-bottom-right-radius: 4px;
    font-size: 0.85rem;
    font-family: "Josefin Sans";
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-around;
    box-shadow: 2px 4px 6px black;

    p {
      transform: translateY(65%);
    }
  }
  .completed {
    text-decoration: line-through;
    color: rgba(255, 255, 255, 0.425);
  }
}
.info {
  color: rgb(167, 167, 167);
  margin: 3% 0;
  font-size: 0.8rem;
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
    .list,
    .subInfos {
      width: 300px;
      .delete {
        padding: 0 110px;
      }
      .checkComplete {
        transform: translate(-1000%, -50%);
      }
    }
  }
}
</style>