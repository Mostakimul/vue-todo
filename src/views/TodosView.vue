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

const toggleComplete = (todoPos) => {
  todos.value[todoPos].isCompleted = !todos.value[todoPos].isCompleted;
};

const toggleEditTodo = (todoPos) => {
  todos.value[todoPos].isEditing = !todos.value[todoPos].isEditing;
};

const updateTodo = (todoVal, todoPos) => {
  todos.value[todoPos].todo = todoVal;
};
</script>

<template>
  <section class="bg-slate-300 rounded-md mt-5 p-5">
    <CommonTitle>Create Todos</CommonTitle>
    <TodoInput @create-todo="createTodo" />
  </section>

  <!-- Todo items -->
  <section v-if="todos.length > 0" class="mt-5">
    <CommonTitle>Todo Items</CommonTitle>
    <ul class="w-2/6 mx-auto">
      <TodoItem
        v-for="(todo, index) in todos"
        :key="todo.id"
        :todo="todo"
        :index="index"
        @toggle-complete="toggleComplete"
        @edit-todo="toggleEditTodo"
        @update-todo="updateTodo"
      />
    </ul>
  </section>
  <!-- No todo msg -->
  <p v-else class="mt-5 text-center">
    You don't have any todos! Please add one.
  </p>
</template>
