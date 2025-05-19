<template>
  <div>
    <input type="text" v-model="task" placeholder="Enter a task..." />
    <button :disabled="!task.trim()" @click="submitTask">ADD TASK</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: '',
    };
  },
  methods: {
    submitTask() {
      this.$emit('add-task', this.task.trim());
      this.task = '';
    },
  },
};
</script>

<style scoped>
input {
  padding: 0.5rem;
  width: 75%;
  height: 25px;
  border-radius: 10px;
  border: none;
}

button {
  height: 44px;
  width: 20%;
  margin-left: 10px;
  padding: 0.5rem 1rem;
  border-radius: 10px;
  border: none;
  font-size: 16px;
  font-weight: 600;
}

button:disabled {
  background-color: #ccc;
}
</style>
