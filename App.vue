<template>
  <div class="container">
    <h1>TaskBuddy</h1>
    
    <!-- CREATE -->
    <div class="task-input-section">
      <input 
        type="text" 
        v-model="newTask"
        placeholder="" 
        class="task-input"
      />
      <button @click="addTask" class="add-task-btn">Add Task</button>
    </div>
    
    <!-- READ -->
    <TaskList 
      :tasks="tasks"
      @toggle-complete="toggleComplete"
      @delete-task="deleteTask"
    />
    
    <!-- COUNTER -->
    <div class="counter-section">
      <p>Count: <span id="count">{{ tasks.length }}</span></p>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import TaskList from './components/Reusable/Tasklist.vue';

export default {
  name: 'App',
  components: {
    TaskList
  },
  setup() {
    const tasks = ref([]);
    const newTask = ref('');

    // CREATE
    const addTask = () => {
      const text = newTask.value.trim();
      if (text === "") return;
      
      tasks.value.push({
        id: Date.now(),
        text: text,
        completed: false
      });
      newTask.value = '';
    };

    // TOGGLE COMPLETE
    const toggleComplete = (taskId) => {
      const task = tasks.value.find(t => t.id === taskId);
      if (task) {
        task.completed = !task.completed;
      }
    };

    // DELETE
    const deleteTask = (taskId) => {
      tasks.value = tasks.value.filter(t => t.id !== taskId);
    };

    return {
      tasks,
      newTask,
      addTask,
      toggleComplete,
      deleteTask
    };
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  background: #b0d4e3;
  margin: 0;
  padding: 0;
}

#app {
  background: #b0d4e3;
  min-height: 100vh;
  padding: 20px;
}

.container {
  width: 80%;
  max-width: 600px;
  margin: 20px auto;
  background: #b0d4e3;
  padding: 20px;
  border-radius: 8px;
}

h1 {
  color: #333;
  margin-bottom: 20px;
  text-align: left;
  font-size: 2rem;
}

.task-input-section {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.task-input {
  flex: 1;
  padding: 10px 15px;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
}

.add-task-btn {
  padding: 10px 20px;
  background: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.2s;
}

.add-task-btn:hover {
  background: #45a049;
}

.counter-section {
  margin-top: 20px;
  padding: 15px;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 4px;
  display: flex;
  align-items: center;
  gap: 15px;
}

.counter-section p {
  margin: 0;
  font-size: 1.1rem;
  font-weight: bold;
}

.increase-btn {
  padding: 8px 15px;
  background: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: background 0.2s;
}

.increase-btn:hover {
  background: #45a049;
}
</style>