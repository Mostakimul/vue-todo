<script setup>
import { uid } from 'uid';
import { computed, ref, watch } from 'vue';
import CommonTitle from '../components/CommonTitle.vue';
import TodoInput from '../components/TodoInput.vue';
import TodoItem from '../components/TodoItem.vue';

const todos = ref([]);

watch(
  todos,
  () => {
    storeTodosInLocalStorage();
  },
  {
    deep: true,
  },
);

const todoCompleted = computed(() => {
  return todos.value.every((todo) => todo.isCompleted);
});

const getTodosFromLocalStorage = () => {
  const storedTodos = JSON.parse(localStorage.getItem('todos'));
  if (storedTodos) {
    todos.value = storedTodos;
  }
};

getTodosFromLocalStorage();

const storeTodosInLocalStorage = () => {
  localStorage.setItem('todos', JSON.stringify(todos.value));
};

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

const deleteTodo = (todoId) => {
  console.log(todoId);
  todos.value = todos.value.filter((todo) => todo.id !== todoId);
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
        @delete-todo="deleteTodo"
      />
    </ul>
  </section>
  <!-- No todo msg -->
  <p v-else class="mt-5 text-center text-red-500">
    You don't have any todos! Please add one.
  </p>

  <!-- complete msg -->
  <p
    v-if="todoCompleted && todos.length > 0"
    class="mt-5 text-center text-green-500"
  >
    You have completed all todos!
  </p>
</template>
