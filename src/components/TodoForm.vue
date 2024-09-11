<script lang="ts" setup>
import { ref } from "vue";

const emits = defineEmits(["addTodo"]);
const todo = ref("");

function clickHandler() {
  if (todo.value != "") emits("addTodo", todo.value);
  todo.value = "";
}
</script>

<template>
  <div
    class="bg-gradient-to-br from-blue-500 to-emerald-300 h-20 flex items-center p-5 gap-10"
  >
    <input class="w-96 rounded h-8 px-3" v-model.trim="todo" />
    <button
      @click="clickHandler"
      class="bg-green-500 rounded py-2 px-3 text-white"
    >
      Add todo
    </button>
  </div>
</template>
