<template>
  <div class="task-input">
    <h1 class="text-2xl font-bold text-gray-800">New Task</h1>
    <input 
      type="text" 
      v-model="newTask"
      @keyup.enter="handleAddTask"
      placeholder="Enter new task..."
    />
    <button 
      @click="handleAddTask"
      class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600"
    >
      Add Task
    </button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'NewTask',
  emits: ['add-task'],
  setup(props, { emit }) {
    const newTask = ref('');

    const handleAddTask = () => {
      const text = newTask.value.trim();
      if (text === "") return;
      
      emit('add-task', text);
      newTask.value = '';
    };

    return {
      newTask,
      handleAddTask
    };
  }
};
</script>

<style scoped>
.task-input {
  margin-bottom: 20px;
}

.task-input h1 {
  margin-bottom: 10px;
  font-size: 1.5rem;
  font-weight: bold;
  color: #1f2937;
}

.task-input input {
  padding: 10px;
  width: 60%;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

.task-input button {
  padding: 10px 16px;
  background: #3b82f6;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.task-input button:hover {
  background: #2563eb;
}
</style>