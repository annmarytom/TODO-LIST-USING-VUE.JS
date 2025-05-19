<template>
    <div class="tasklist-div">
        <h2>{{ title }}</h2>
        <div v-if="tasks.length">
            <TaskItem v-for="task in tasks" :key="task.id" :task="task" @delete-task="$emit('delete-task', task.id)"
                @toggle-status="$emit('toggle-status', task.id)" />
        </div>
        <div v-else>
            <img src="../assets/ae8ac2fa217d23aadcc913989fcc34a2.jpg" alt="Empty" width="150" />

        </div>
    </div>
</template>

<script>
import TaskItem from './TaskItem.vue';

export default {
    props: ['tasks', 'title'],
    components: { TaskItem },
};
</script>

<style scoped>
.tasklist-div {
    background-color: rgb(243, 239, 224);
    border-radius: 10px;
}

img {
    margin-top: 10px;
    opacity: 0.5;
}
</style>