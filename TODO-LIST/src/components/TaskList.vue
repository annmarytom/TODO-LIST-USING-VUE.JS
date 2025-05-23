<template>
    <div class="tasklist-div">
        <h2>{{ title }}</h2>
        <div v-if="tasks.length">
            <TaskItem v-for="task in tasks" :key="task.id" :task="task" @delete-task="$emit('delete-task', task.id)"
                @toggle-status="$emit('toggle-status', task.id)" />
        </div>
        
        <div v-else>
            <img src="../assets/folder.jpg" alt="Empty" width="150" />

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
    background-color:#2a3184;
    border-radius: 40px;
    padding: 0px 20px 20px 20px;
    margin: 10px 0px;
    
}

img {
    margin-top: 10px;
    opacity: 0.5;
}
</style>