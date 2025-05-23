<template>
    <div>
      <TaskInput @add-task="addTask" />
      <TaskList
        title="Tasks"
        :tasks="tasks"
        @delete-task="deleteTask"
        @toggle-status="toggleStatus"
      />
    </div>
  </template>
  
  <script>
  import TaskInput from '../components/TaskInput.vue';
  import TaskList from '../components/TaskList.vue';
  
  export default {
    props: ['tasks'],
    components: { TaskInput, TaskList },
    emits: ['add-task', 'delete-task', 'toggle-status'],
    methods: {
      addTask(task) {
        this.$emit('add-task', task);
      },
      deleteTask(id) {
        this.$emit('delete-task', id);
      },
      toggleStatus(id) {
        this.$emit('toggle-status', id);
      },
    },
  };
  </script>
  