// pages/index.vue
<template>
  <div class="flex flex-col items-center justify-center bg-gray-100 p-4">
    <h1 class="text-3xl font-bold mb-6">Todo List</h1>
    <div class="bg-white shadow-lg rounded-lg p-6 w-full max-w-md">
      <TodoForm />
    </div>
    <div class="mt-6 w-full max-w-md">
      <div v-for="todo in store.todos" :key="todo.id" class="bg-white shadow-md rounded-lg p-4 mb-4">
        <TodoItem :todo="todo" />
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { useTodoStore } from '@/store/todo';
import TodoItem from '@/components/TodoItem.vue';
import TodoForm from '@/components/TodoForm.vue';

const store = useTodoStore();
</script>
