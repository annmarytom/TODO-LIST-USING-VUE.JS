<template>
  <div class="container">
    <h1>To-Do List</h1>
    <TaskInput @add-task="addTask" />

    <div class="status">
      ✅ Completed: {{ completedTasks.length }} | 
      ❌ Incomplete: {{ incompleteTasks.length }}
    </div>

    <TaskList title="Incomplete Tasks" :tasks="incompleteTasks" @delete-task="deleteTask"
      @toggle-status="toggleStatus" />

    <TaskList title="Completed Tasks" :tasks="completedTasks" @delete-task="deleteTask" @toggle-status="toggleStatus" />
  </div>
</template>

<script>
import TaskInput from './components/TaskInput.vue';
import TaskList from './components/TaskList.vue';

export default {
  components: { TaskInput, TaskList },
  data() {
    return {
      tasks: [],
    };
  },
  computed: {
    completedTasks() {
      return this.tasks.filter(task => task.completed);
    },
    incompleteTasks() {
      return this.tasks.filter(task => !task.completed);
    },
  },
  methods: {
    addTask(taskText) {
      this.tasks.push({
        id: Date.now(),
        text: taskText,
        completed: false,
      });
      this.saveTasks();
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
      this.saveTasks();
    },
    toggleStatus(id) {
      const task = this.tasks.find(task => task.id === id);
      if (task) task.completed = !task.completed;
      this.saveTasks();
    },
  
  saveTasks() {
      localStorage.setItem('vue-tasks', JSON.stringify(this.tasks));
    },
    loadTasks() {
      const stored = localStorage.getItem('vue-tasks');
      if (stored) {
        this.tasks = JSON.parse(stored);
      }
    },
  },
  created() {
    this.loadTasks(); 
  },
};
</script>

<style>
.container {
  max-width: 600px;
  margin: auto;
  padding: 1rem;
  font-family: sans-serif;
  text-align: center;
  background-color: #1a1c84;
  border: 5px solid white;
  border-radius: 10px;
}
.container h1{
  color: #FFD700;
}
.status {
  margin: 1rem 0;
  color:whitesmoke;
  display: flex;
  gap:20px;
  justify-content: center;
  align-items: center;
}
</style>
