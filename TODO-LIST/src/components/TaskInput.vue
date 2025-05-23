<template>
  <div class="input-area">
    <input type="text" v-model="task" placeholder="Enter a task..." />
    <button :disabled="!task.trim()" @click="submitTask">+</button>
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
.input-area {
  position: relative;
  padding: 3px;
}

input {
  padding: 0.5rem;
  width: 97%;
  height: 40px;
  border-radius: 40px;
  border: none;
  background-color: rgb(4 28 2 / 19%);
  color: white;
  font-size: 20px;
}

button {
  position: absolute;
  top: 13px;
  left: 550px;
  height: 35px;
  width: 6%;
  padding: 0.4rem;
  border-radius: 30px;
  border: none;
  font-size: 20px;
  font-weight: 600;
  background-color: #A0C4FF;
  color: white;
  cursor: pointer;
}

button:disabled {
  background-color: #3e79ae;
  color: gray;
  border: none;

}
</style>
