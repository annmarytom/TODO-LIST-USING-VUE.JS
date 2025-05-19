<template>
  <div class="task">
    <input type="checkbox" :checked="task.completed" @change="$emit('toggle-status')" />
    <span :class="{ done: task.completed }">{{ task.text }}</span>
    <button @click="$emit('delete-task')"><i class="ri-delete-bin-line delete-icon"></i></button>
  </div>
</template>

<script>
export default {
  props: ['task'],
};
</script>

<style scoped>
.task {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem;
  border-bottom: 1px solid #ccc;
}

.done {
  text-decoration: line-through;
  color: gray;
}

button {
  background: none;
  border: none;
  cursor: pointer;
}

.delete-icon {
  color: red;
  font-size: 20px;
}
</style>
