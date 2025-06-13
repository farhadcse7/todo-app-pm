<script setup>
defineProps({
    index: {
        type: Number
    },
    todo: {
        type: Object
    }
})
const checkComplete = (index) => {
    todos[index].completed = !todos[index].completed;
};

const removeTodo = (index) => {
    todos.splice(index, 1);
};
</script>

<template>
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
</template>