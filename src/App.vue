<script setup>
import { reactive, ref, computed } from 'vue';

const todo = ref("");

const todos = reactive(
  [
    { id: 1, title: 'Buy groceries', completed: false },
    { id: 2, title: 'Walk the dog', completed: true },
    { id: 3, title: 'Read a book', completed: false }
  ]
);

const addTodo = () => {
  // console.log('Adding todo');

  if (todo.value === '') {
    return;
  }

  todos.push({
    id: todos.length + 1,
    title: todo.value,
    completed: false
  });
  todo.value = '';
};

const checkComplete = (index) => {
  todos[index].completed = !todos[index].completed;
};

const removeTodo = (index) => {
  todos.splice(index, 1);
};

const countAllTodo = computed(() => {
  return todos.length;
});
const countCompletedTodo = computed(() => {
  return todos.filter(todo => todo.completed).length;
});

</script>

<template>
  <div class="max-w-md mx-auto bg-white shadow-lg rounded-lg overflow-hidden mt-16 border p-6 space-y-6">
    <h1 class="text-2xl uppercase text-gray-700 font-bold">
      To Do List <span v-if="todos.length">({{ countCompletedTodo }}/{{ countAllTodo }})</span> </h1>
    <!-- {{ todos }} -->
    <!-- {{ todo }} -->
    <form @submit.prevent="addTodo">
      <div class="flex items-center border-b-2 border-teal-500 py-2">
        <input v-model="todo" class="border-none focus:outline-none w-full text-gray-700" type="text"
          placeholder="Add a task">
        <button
          class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-4 text-sm hover:border-teal-700 text-white py-1 px-2 rounded"
          type="submit">Add</button>
      </div>
    </form>
    <ul v-if="todos.length">
      <li v-for="(todo, index) in todos" :key="todo.id">
        <div class="flex items-center justify-between mt-4">
          <div class="flex items-center">
            <input @input="checkComplete(index)" :checked="todo.completed"
              class="h-4 w-4 text-teal-600 focus:ring-teal-500 border-gray-300 rounded" type="checkbox" name="todo"
              :id="`todo-${todo.id}`">
            <label class="ml-3 block to-green-900" :for="`todo-${todo.id}`"
              :class="{ 'line-through text-gray-400': todo.completed }">
              <span class="text-lg font-medium">{{ todo.title }} </span>
            </label>
          </div>
          <button @click="removeTodo(index)" class="flex-shrink-0">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
              stroke-linecap="round" stroke-linejoin="round">
              <polyline points="3 6 5 6 21 6" />
              <path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h2a2 2 0 0 1 2 2v2" />
              <line x1="10" y1="11" x2="10" y2="17" />
              <line x1="14" y1="11" x2="14" y2="17" />
            </svg>
          </button>
        </div>
      </li>
    </ul>
    <div v-else>
      <p>No tasks yet</p>
    </div>
  </div>
</template>

<style scoped>
</style>
