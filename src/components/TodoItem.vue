<script setup lang="ts">
import { computed, inject } from "vue";
import { Todo } from "../App.vue";
const { todo } = defineProps<{
  todo: Todo;
}>();

const deleteTodo = inject<(id: number) => void>("deleteTodo");
const toggleCheck = inject<(id: number) => void>("toggleCheck");

function handleDelete() {
  deleteTodo && deleteTodo(todo.id);
}

const isChecked = computed(() => todo.checked);
</script>

<template>
  <li class="flex items-center gap-3">
    <input
      :checked="todo.checked"
      v-on:change="toggleCheck && toggleCheck(todo.id)"
      :id="`${todo.id}`"
      type="checkbox"
    />
    <label
      :for="`${todo.id}`"
      class="select-none cursor-pointer text-blue-800 text-lg"
      :class="isChecked && 'line-through'"
      >{{ todo.title }}</label
    >
    <button
      @click="handleDelete"
      class="text-white bg-red-500 text-sm py-2 px-3 rounded hover:bg-red-500/70"
    >
      Delete
    </button>
  </li>
</template>
