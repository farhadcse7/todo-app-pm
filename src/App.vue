<script setup>
import { reactive, ref, computed } from 'vue';
import SingleTodo from './components/SingleTodo.vue';

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
        <SingleTodo :index="index" :todo="todo" />
      </li>
    </ul>
    <div v-else>
      <p>No tasks yet</p>
    </div>
  </div>
</template>

<style scoped></style>
