<template>
    <TaskList
      title="Incomplete Tasks"
      :tasks="tasks.filter(t => !t.completed)"
      @delete-task="$emit('delete-task', $event)"
      @toggle-status="$emit('toggle-status', $event)"
    />
  </template>
  
  <script>
  import TaskList from '../components/TaskList.vue';
  
  export default {
    props: ['tasks'],
    components: { TaskList },
    emits: ['delete-task', 'toggle-status'],
  };
  </script>
  