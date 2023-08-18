<template>
  <div class="task">
    
    <h3>{{ task.title }}</h3>
    <div class="icons">
        <i class="material-icons" @click="TaskStore.deleteTask(task.id)">
            delete
        </i>
        <i 
        :class = "{active: task.isFav}"
        class="material-icons" @click="TaskStore.toggleFav(task.id)">
            favorite
        </i>
    </div>
  </div>
</template>

<script>
import { useTaskStore } from '../stores/TaskStore';

export default {
    name: 'TaskDetails', 
    props: ['task'],
    setup(){
        const TaskStore = useTaskStore();

        return {TaskStore}
    }
}
</script>

<style>

</style>