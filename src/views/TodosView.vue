<script setup>
import { uid } from 'uid';
import { ref } from 'vue';
import TodoInput from '../components/TodoInput.vue';

const todos = ref([]);
const createTodo = (todo) => {
  todos.value.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null,
  });
};
</script>

<template>
  <section class="bg-slate-300 rounded-md mt-5 p-5">
    <h1 class="font-semibold text-center text-xl">Create Todos</h1>
    <TodoInput @create-todo="createTodo" />
  </section>
</template>
