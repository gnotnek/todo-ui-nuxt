<template>
  <div>
    <ToDoList :todos="todos" />
  </div>
</template>

<script setup>
import ToDoList from '~/components/TodoList.vue';

const todos = ref([])
</script>