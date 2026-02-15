<template>
  <div class="task-list">
    <div
      v-for="task in tasks" 
      :key="task.id"
      class="task-item"
      :class="{ completed: task.completed }"
    >
      <span class="task-text">{{ task.text }}</span>
      <div class="actions">
        <button
          class="complete-btn" 
          @click="$emit('toggle-complete', task.id)"
        >
          {{ task.completed ? 'Completed' : 'Complete' }}
        </button>
        <button
          class="delete-btn" 
          @click="$emit('delete-task', task.id)"
        >
          Delete
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskList',
  props: {
    tasks: {
      type: Array,
      required: true
    }
  },
  emits: ['toggle-complete', 'delete-task']
};
</script>

<style scoped>
.task-list {
  margin-bottom: 20px;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 15px;
  background: rgba(255, 255, 255, 0.7);
  margin-bottom: 10px;
  border-radius: 4px;
  transition: background-color 0.2s;
}

.task-item:hover {
  background: rgba(255, 255, 255, 0.9);
}

.task-text {
  flex: 1;
  font-size: 1rem;
  color: #333;
}

.task-item.completed .task-text {
  text-decoration: line-through;
  color: #999;
}

.actions {
  display: flex;
  gap: 10px;
}

.complete-btn,
.delete-btn {
  padding: 6px 12px;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  font-weight: bold;
  font-size: 0.9rem;
  transition: all 0.2s;
}

.complete-btn {
  background: #4caf50;
  color: white;
}

.complete-btn:hover {
  background: #45a049;
}

.delete-btn {
  background: #f44336;
  color: white;
}

.delete-btn:hover {
  background: #da190b;
}
</style>