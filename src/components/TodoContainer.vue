<script setup lang="ts">
import TodoItem from "./TodoItem.vue";
import { Todo } from "../App.vue";

defineProps<{ todos: Todo[] }>();
</script>

<template>
  <div class="h-[calc(100vh-5rem)] p-6">
    <ul v-if="todos.length > 0" class="flex flex-col gap-7 w-[600px]">
      <TodoItem :key="todo.id" v-for="todo in todos" :todo="todo" />
    </ul>
    <h2 v-else class="text-2xl text-blue-800">No todos yet</h2>
  </div>
</template>
