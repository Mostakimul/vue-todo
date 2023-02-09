<script setup>
import { Icon } from '@iconify/vue';

const props = defineProps({
  todo: {
    type: Object,
    required: true,
    // default: It will only works string, number or boolean
  },
  index: {
    type: Number,
    required: true,
  },
});

const emit = defineEmits(['toggle-complete', 'edit-todo', 'update-todo']);

const editTodo = (index) => {
  emit('edit-todo', index);
};
</script>

<template>
  <li
    class="flex items-center justify-between gap-4 bg-gray-300 px-3 py-2 rounded-md group"
  >
    <div class="flex items-center gap-5">
      <!-- checkbox -->
      <input
        :checked="todo.isCompleted"
        @input="$emit('toggle-complete', index)"
        type="checkbox"
        class="appearance-none w-5 h-5 bg-white rounded-full shadow-md checked:bg-green-500"
      />
      <!-- input and text div -->
      <div>
        <input
          v-if="todo.isEditing"
          @input="$emit('update-todo', $event.target.value, index)"
          type="text"
          :value="todo.todo"
          class="rounded p-1 border-2 border-green-600"
        />
        <p v-else :class="{ 'line-through': todo.isCompleted }">
          {{ todo.todo }}
        </p>
      </div>
    </div>
    <!-- icons div -->
    <div class="items-center gap-2 group-hover:flex hidden">
      <Icon
        v-if="todo.isEditing"
        @click="editTodo(index)"
        class="cursor-pointer"
        icon="ph:check-circle"
        color="#41b080"
        width="20"
      />
      <Icon
        v-else
        @click="editTodo(index)"
        class="cursor-pointer"
        icon="ph:pencil-fill"
        color="#41b080"
        width="20"
      />
      <Icon class="cursor-pointer" icon="ph:trash" color="#f95e5e" width="20" />
    </div>
  </li>
</template>
