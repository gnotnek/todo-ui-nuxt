<template>
  <div>
    <ToDoList :todos="todos" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'
import ToDoList from '~/components/ToDoList.vue';

const todos = ref([])
axios.get('http://localhost:3500/todos').then((response) => {
  todos.value = response.data
})
</script>