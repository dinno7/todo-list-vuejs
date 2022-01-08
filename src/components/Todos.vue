<template>
  <div>
    <transition name="fade-top" appear="">
      <h1>Todo list</h1>
    </transition>
    <div class="todos">
      <div class="input">
        <input
          ref="todoInput"
          type="text"
          v-model="newTodo"
          @keypress.enter="addTodo"
          placeholder="Add a new todo..."
        />
        <div class="top-border"></div>
        <button class="add-btn" @click="addTodo">Add</button>
      </div>
      <transition name="switch" mode="out-in">
        <div v-if="todos.length">
          <transition-group
            tag="ul"
            name="list"
            mode="out-in"
            @enter="todoEnter"
          >
            <li v-for="todo in todos" :key="todo.id" class="todo">
              {{ todo.text }}
              <div class="delete-todo" @click="deleteTodo(todo.id)">
                &times;
              </div>
            </li>
          </transition-group>
        </div>
        <div v-else style="margin-top: 30px;">Woohoo, nothing left todo!</div>
      </transition>
    </div>
    <transition name="fade">
      <p
        v-show="addLog"
        class="added-log"
        @before-leave="leaveAddLog"
        @click="addLog = false"
      >
        Added successfully.
      </p>
    </transition>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";

export default {
  setup(props, { emit }) {
    //  { text: "make the bed", id: 1 },
    // { text: "play video games", id: 2 },
    const todos = ref([]);
    todos.value = JSON.parse(localStorage.getItem("todos"))
      ? JSON.parse(localStorage.getItem("todos"))
      : [];
    const newTodo = ref("");
    const addLog = ref(false);
    const todoInput = ref(null);

    const addTodo = () => {
      if (newTodo.value) {
        const id = Math.random();
        todos.value.push({ text: newTodo.value, id }); // add end of list
        // todos.value = [{ text: newTodo.value, id }, ...todos.value]; //Add start of list
        localStorage.setItem("todos", JSON.stringify(todos.value));
        newTodo.value = "";
      } else {
        emit("badValue");
      }
    };

    const deleteTodo = (id) => {
      todos.value = todos.value.filter((todo) => todo.id != id);
      localStorage.setItem("todos", JSON.stringify(todos.value));
    };
    const todoEnter = () => {
      addLog.value = true;
      setTimeout(() => {
        addLog.value = false;
      }, 3000);
    };
    onMounted(() => {
      todoInput.value.focus();
    });
    return {
      todos,
      addTodo,
      deleteTodo,
      newTodo,
      addLog,
      todoEnter,
      todoInput,
    };
  },
};
</script>

<style>
.todos {
  max-width: 400px;
  margin: 20px auto;
  position: relative;
}
.added-log {
  width: 400px;
  margin: 20px auto;
  background: var(--green);
  color: #fff;
  padding: 7px 0;
  border-radius: 10px;
  position: fixed;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  cursor: pointer;
  z-index: 999;
}
.top-border {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: var(--green);
  transform: scaleX(0);
  transform-origin: center;
  transition: all 0.3s ease-in-out;
}
.input {
  position: relative;
  height: 2.7rem;
}
input {
  width: 100%;
  height: 100%;
  padding: 0 12px;
  border: 1px solid #eee;
  border-radius: 10px;
  margin-bottom: 20px;
  box-sizing: border-box;
  transition: all 0.2s ease;
  caret-color: var(--green);
}

input:focus ~ .top-border {
  transform: scaleX(1);
}
input:focus {
  outline: none;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
.add-btn {
  cursor: pointer;
  border: 0;
  outline: none;
  padding: 10px;
  border-radius: 10px;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
  background: var(--green);
  color: #fff;
  position: absolute;
  right: 0;
  height: 100%;
  font-weight: 500;
  font-size: 1rem;
}
.add-btn:hover,
.add-btn:focus {
  opacity: 0.8;
}
input:focus ~ .add-btn {
  border-top-right-radius: 0;
}
.todos ul {
  position: relative;
  padding: 0;
}
.todos li {
  list-style-type: none;
  display: block;
  margin-bottom: 10px;
  padding: 10px;
  background: white;
  box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  width: 100%;
  box-sizing: border-box;
  transition: all 0.3s ease;
  user-select: none;
}
.todos li:hover {
  background: var(--green);
  color: #fff;
  transform: scale(1.1);
}
.delete-todo {
  font-size: 25px;
  position: absolute;
  right: 2%;
  transform: translateY(-25px);
  transition: all 0.2s ease;
  color: var(--gray);
  padding: 0 7px;
  border-radius: 7px;
}
.delete-todo:hover {
  background: var(--red);
  border: 0;
  color: white;
}
.todos li:hover {
  cursor: pointer;
}

/* //------Transitions: */
.list-enter-from {
  opacity: 0;
  transform: list(0.6);
}
/* .list-enter-to {
  opacity: 1;
  transform: scale(1);
} */
/* .list-leave-from {
  opacity: 1;
  transform: scale(1);
} */
.list-leave-to {
  opacity: 0;
  transform: scale(0.6);
}
.list-enter-active {
  transition: all 0.4s ease;
}
.list-leave-active {
  transition: all 0.4s ease;
  position: absolute;
}
.list-move {
  transition: all 0.4s ease;
}
/* ---------------- */
.switch-enter-from,
.switch-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
.switch-enter-active,
.switch-leave-active {
  transition: all 0.3s ease;
}
/* ------------------------ */
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s ease;
}
</style>
