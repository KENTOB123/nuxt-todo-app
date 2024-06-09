<template>
  <div>
    <h1>TODOリスト</h1>
    <ul>
      <li v-for="todo in todos" :key="todo.id">
        <input
          type="checkbox"
          v-model="todo.completed"
          @change="toggleTodo(todo.id)"
        />
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button @click="removeTodo(todo.id)">削除</button>
      </li>
    </ul>
    <input v-model="newTodo" @keyup.enter="addTodo" />
    <button @click="addTodo">追加</button>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { useTodoStore } from "~/stores/todo";

const todoStore = useTodoStore();
const newTodo = ref("");

const addTodo = () => {
  if (newTodo.value.trim()) {
    todoStore.addTodo(newTodo.value);
    newTodo.value = "";
  }
};

const removeTodo = (id: number) => {
  todoStore.removeTodo(id);
};

const toggleTodo = (id: number) => {
  todoStore.toggleTodo(id);
};

const todos = todoStore.todos;
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}vujs
</style>
