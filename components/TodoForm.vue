<template>
  <form @submit.prevent="addTodo">
    <input v-model="text" type="text" placeholder="New Todo" class="border p-2 mr-2" />
    <button type="submit" class="bg-blue-500 text-white px-4 py-2">Add</button>
  </form>
</template>
  
<script setup lang="ts">
  import { ref } from 'vue';
  import { useTodoStore } from '@/store/todo';

  const store = useTodoStore();
  const text = ref('');

  const addTodo = () => {
  if (text.value.trim()) {
      store.addTodo(text.value);
      text.value = '';
  }
};
</script>