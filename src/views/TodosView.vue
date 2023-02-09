<script setup>
import { uid } from 'uid';
import { ref } from 'vue';
import CommonTitle from '../components/CommonTitle.vue';
import TodoInput from '../components/TodoInput.vue';
import TodoItem from '../components/TodoItem.vue';

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
    <CommonTitle>Create Todos</CommonTitle>
    <TodoInput @create-todo="createTodo" />
  </section>

  <!-- Todo items -->
  <section class="mt-5">
    <CommonTitle>Todo Items</CommonTitle>
    <ul class="w-2/6 mx-auto">
      <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" />
    </ul>
  </section>
</template>
