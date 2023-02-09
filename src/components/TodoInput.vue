<script setup>
import { reactive } from 'vue';
import TodoButton from './TodoButton.vue';
// reactive using ref
const todoState = reactive({
  todo: '',
  invalid: null,
  errMsg: '',
});

const emit = defineEmits(['create-todo']);

const createTodo = () => {
  todoState.invalid = null;
  if (todoState.todo !== '') {
    emit('create-todo', todoState.todo);
    todoState.todo = '';
    return;
  }
  todoState.invalid = true;
  todoState.errMsg = 'You must enter todo value';
};
</script>

<template>
  <div class="flex justify-center items-start py-5">
    <div>
      <input
        v-model="todoState.todo"
        type="text"
        class="rounded-md p-1 shadow-md"
      />
      <p v-show="todoState.invalid" class="text-red-500">
        {{ todoState.errMsg }}
      </p>
    </div>
    <TodoButton @click="createTodo">Create</TodoButton>
  </div>
</template>
