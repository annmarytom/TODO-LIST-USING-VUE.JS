

<template>
  <div class="container">
    <h1>To-Do List</h1>

    <!-- Navigation -->
    <nav class="nav">
      <a href="#/" :class="{ active: view === 'all' }"> Tasks</a>
      <a href="#/completed" :class="{ active: view === 'completed' }"> Completed</a>
      <a href="#/incomplete" :class="{ active: view === 'incomplete' }"> Incomplete</a>
    </nav>

    
    <div class="status">
      ✅ Completed: {{ completedTasks.length }} |
      ❌ Incomplete: {{ incompleteTasks.length }}
    </div>

  
    <component
      :is="currentView"
      :tasks="tasks"
      @add-task="addTask"
      @delete-task="deleteTask"
      @toggle-status="toggleStatus"
    />
  </div>
</template>

<script>
import Tasks from './pages/tasks.vue';
import CompletedTasks from './pages/completed.vue';
import IncompleteTasks from './pages/incompleted.vue';

export default {
  components: { Tasks, CompletedTasks, IncompleteTasks },
  data() {
    return {
      view: 'all', // default route
      tasks: [],
    };
  },
  computed: {
    currentView() {
      return {
        all: 'Tasks',
        completed: 'CompletedTasks',
        incomplete: 'IncompleteTasks',
      }[this.view];
    },
    completedTasks() {
      return this.tasks.filter(task => task.completed);
    },
    incompleteTasks() {
      return this.tasks.filter(task => !task.completed);
    },
  },
  methods: {
    
    addTask(taskText) {
      this.tasks.push({ id: Date.now(), text: taskText, completed: false });
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
      if (stored) this.tasks = JSON.parse(stored);
    },

    updateViewFromHash() {
      const hash = window.location.hash;
      if (hash.includes('completed')) {
        this.view = 'completed';
      } else if (hash.includes('incomplete')) {
        this.view = 'incomplete';
      } else {
        this.view = 'all';
      }
    }
  },
  created() {
    this.loadTasks();
    this.updateViewFromHash();
    window.addEventListener('hashchange', this.updateViewFromHash);
  },
  beforeUnmount() {
    window.removeEventListener('hashchange', this.updateViewFromHash);
  }
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
.container h1 {
  color: #FFD700;
}
.status {
  margin: 1rem 0;
  color: whitesmoke;
  display: flex;
  gap: 20px;
  justify-content: center;
  align-items: center;
}
.nav {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 1rem;
} 
.nav a {
  padding: 0.5rem 1rem;
  border-radius: 20px;
  background-color: #A0C4FF;
  color: black;
  text-decoration: none;
  font-weight: bold;
}
.nav a.active {
  background-color: #FFD700;
}
</style>
