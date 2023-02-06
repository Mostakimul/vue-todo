<script setup>
import { defineEmits, reactive } from 'vue';
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
    <button
      @click="createTodo"
      class="px-5 bg-green-500 rounded-md mx-5 py-1 ring-1 ring-gray-800 font-semibold shadow-md"
    >
      Create
    </button>
  </div>
</template>
