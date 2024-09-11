<script setup lang="ts">
import { ref } from "vue";
import TodoForm from "./components/TodoForm.vue";

type Todo = {
  id: number;
  title: string;
  checked: boolean;
};

const todos = ref<Todo[]>([]);
</script>

<template>
  <div class="h-screen">
    <TodoForm />
  </div>
</template>
