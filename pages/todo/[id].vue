<template>
    <div class="flex flex-col items-center justify-center bg-gray-100 p-4">
      <div class="bg-white shadow-lg rounded-lg p-6 w-full max-w-md text-center">
        <h1 class="text-3xl font-bold mb-4">Todo Details<NuxtLink :to="`/`">↩</NuxtLink></h1>
        <div v-if="todo">
          <h2 class="text-lg font-semibold mb-2">{{ todo.text }}</h2>
          <p class="mb-4">Status: 
            <span :class="{ 'text-green-500': todo.completed, 'text-red-500': !todo.completed }">
              {{ todo.completed ? 'Completed' : 'Pending' }}
            </span>
          </p>
          <button @click="toggleTodo" class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 transition">Toggle Status</button>
        </div>
        <div v-else>
          <p class="text-red-500">Todo not found.</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { useRoute } from 'vue-router';
  import { useTodoStore } from '@/store/todo';
  import { ref, watchEffect } from 'vue';
  
  // Get store and route
  const route = useRoute();
  const store = useTodoStore();
  const todo = ref<{ id: number; text: string; completed: boolean } | null>(null);
  
  // Fetch the todo (Works in SSR and client)
  const { data } = await useAsyncData(`todo-${route.params.id}`, async () => {
    return store.todos.find(t => t.id === Number(route.params.id)) || null;
  });
  
  // Set the todo value
  todo.value = data.value;
  
  // Watch for changes when navigating
  watchEffect(() => {
    todo.value = store.todos.find(t => t.id === Number(route.params.id)) || null;
  });
  
  const toggleTodo = () => {
    if (todo.value) {
      store.toggleTodo(todo.value.id);
    }
  };
  </script>
  