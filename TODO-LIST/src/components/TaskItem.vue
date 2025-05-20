<template>
  <div class="task">
    <div class="input-area">
      <input type="checkbox" :checked="task.completed" @change="$emit('toggle-status')" />
      <span :class="{ done: task.completed }">{{ task.text }}</span>
    </div>
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
  /* border-bottom: 1px solid #ccc; */
  color: rgb(212, 206, 206);
  ;
}
.input-area{
  display: flex;
  
  gap:10px;
}
.done {
  text-decoration: line-through;
  color: rgb(212, 206, 206);
}

button {
  background: none;
  border: none;
  cursor: pointer;
}

.delete-icon {
  color: rgb(247, 232, 232);
  font-size: 20px;
}
</style>
