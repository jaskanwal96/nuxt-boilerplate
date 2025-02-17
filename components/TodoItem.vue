<template>
    <div class="p-4 border rounded-md flex justify-between items-center">
      <span :class="{ 'line-through': todo.completed }">{{ todo.text }}</span>
      <div>
        <NuxtLink :to="`/todo/${todo.id}`">ℹ️</NuxtLink>
        <button @click="toggleTodo" class="mr-2">✔️</button>
        <button @click="removeTodo">❌</button>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { defineProps } from 'vue';
  import { useTodoStore } from '@/store/todo';
  const store = useTodoStore();
  const props = defineProps<{ todo: { id: number; text: string; completed: boolean } }>();
  
  const toggleTodo = () => store.toggleTodo(props.todo.id);
  const removeTodo = () => store.removeTodo(props.todo.id);
  </script>