<template>
  <div id="app">
    <h1>Todo List</h1>
    <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new task" />
    <button @click="addTodo">Add</button>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.done" @change="toggleTodoStatus(index)" />
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
    <p>{{ remainingTodos }} tasks remaining</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useTodoStore } from './stores/todoStore';

const newTodo = ref('');
const todoStore = useTodoStore();

const addTodo = () => {
  if (newTodo.value.trim()) {
    todoStore.addTodo(newTodo.value);
    newTodo.value = '';
  }
};

const removeTodo = (index) => {
  todoStore.removeTodo(index);
};

const toggleTodoStatus = (index) => {
  todoStore.toggleTodoStatus(index);
};

const todos = todoStore.todos;
const remainingTodos = todoStore.remainingTodos;
</script>

<style scoped>
/* Latar Belakang dan Penataan Umum */
#app {
  font-family: 'Arial', sans-serif;
  max-width: 600px;
  margin: 2rem auto;
  padding: 2rem;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

/* Judul */
h1 {
  font-size: 2rem;
  margin-bottom: 1rem;
  color: #333;
}

/* Input dan Tombol */
input[type="text"] {
  width: calc(100% - 100px);
  padding: 10px;
  font-size: 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  margin-right: 10px;
}

button {
  padding: 10px 20px;
  font-size: 1rem;
  color: white;
  background-color: #84ff00;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}

/* Daftar Tugas */
ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ddd;
  transition: background-color 0.3s;
}

li:hover {
  background-color: #f1f1f1;
}

/* Checkbox dan Teks Tugas */
input[type="checkbox"] {
  margin-right: 10px;
}

span {
  flex-grow: 1;
  font-size: 1rem;
}

.done {
  text-decoration: line-through;
  color: #999;
}

/* Tombol Hapus */
li button {
  background-color: #dc3545;
  border: none;
  color: white;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

li button:hover {
  background-color: #c82333;
}

/* Pesan Tugas Tersisa */
p {
  font-size: 1rem;
  color: #666;
  margin-top: 1rem;
}

/* Responsif untuk Layar Kecil */
@media (max-width: 600px) {
  #app {
    padding: 1rem;
  }

  input[type="text"] {
    width: calc(100% - 80px);
  }

  button {
    padding: 10px;
    width: 80px;
  }
}
</style>

