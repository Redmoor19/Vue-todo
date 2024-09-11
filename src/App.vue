<script setup lang="ts">
import { provide, ref, watchEffect } from "vue";
import TodoForm from "./components/TodoForm.vue";
import TodoContainer from "./components/TodoContainer.vue";

export type Todo = {
  id: number;
  title: string;
  checked: boolean;
};

const todos = ref<Todo[]>(getFromLocal());

function getFromLocal() {
  const localTodos = localStorage.getItem("todos");
  if (localTodos != null) {
    return JSON.parse(localTodos);
  }
  return [];
}

watchEffect(() => {
  localStorage.setItem("todos", JSON.stringify(todos.value));
});

provide<(id: number) => void>("deleteTodo", deleteTodo);
provide<(id: number) => void>("toggleCheck", toggleCheck);

function addTodo(title: string) {
  const todoItem: Todo = {
    title,
    id: Date.now(),
    checked: false,
  };
  todos.value.push(todoItem);
}

function deleteTodo(id: number) {
  todos.value = todos.value.filter((todo) => todo.id !== id);
}

function toggleCheck(id: number) {
  todos.value = todos.value.map((item) =>
    item.id === id ? { ...item, checked: !item.checked } : item
  );
}
</script>

<template>
  <div class="h-screen">
    <TodoForm @addTodo="addTodo" />
    <TodoContainer :todos="todos" />
  </div>
</template>
