<template>
  <div class="max-w-xl mx-auto p-4 bg-gray-200 rounded-lg shadow-md">
    <h1 class="text-2xl font-bold mb-4">Todo List</h1>
    <div class="mb-4">
      <input
        v-model="newTodo.title"
        @keyup.enter="addTodo"
        type="text"
        placeholder="Todo title"
        class="w-full p-2 border border-gray-300 rounded-md"
      />
      <input
        v-model="newTodo.description"
        @keyup.enter="addTodo"
        type="text"
        placeholder="Todo description"
        class="w-full p-2 border border-gray-300 rounded-md"
      />
      <button
        @click="addTodo"
        class="mt-2 w-full bg-gray-600 text-white p-2 rounded-md"
      >
        Add
      </button>
    </div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        :key="index"
        class="flex items-center justify-between bg-gray-100 p-2 mb-2 rounded-md shadow"
      >
        <div class="flex items-center">
          <input
            type="checkbox"
            v-model="todo.completed"
            class="mr-2"
          />
          <span :class="{ 'line-through': todo.completed }">{{ todo.title }}</span>
        </div>
        <div class="flex items-center">
          <button
            @click="editTodo(index)"
            class="mr-2 bg-yellow-500 text-white px-2 py-1 rounded-md"
          >
            Edit
          </button>
          <button
            @click="viewTodo(todo)"
            class="mr-2 bg-blue-500 text-white px-2 py-1 rounded-md"
          >
            View
          </button>
          <button
            @click="deleteTodo(index)"
            class="bg-red-500 text-white px-2 py-1 rounded-md"
          >
            Delete
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
const todos = ref([])
const newTodo = ref('')

await useFetch('http://localhost:3500/todos', {
  then: (data) => {
    todos.value = data
  }
})

const addTodo = () => {
  if (newTodo.value.trim() === '') {
    return
  }

  todos.value.push({
    title: newTodo.value,
    description: newTodo.value,
    completed: false
  })

  newTodo.value = ''
}

const deleteTodo = (index) => {
  todos.value.splice(index, 1)
}

const editTodo = (index) => {
  const todo = todos.value[index]
  const newText = prompt('Edit todo', todo.text)

  if (newText === null) {
    return
  }

  todo.text = newText
}

const viewTodo = (todo) => {
  alert(todo.description)
}
</script>

<style>
.line-through {
  text-decoration: line-through;
}
</style>
