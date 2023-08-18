<template>
  <main>
    <!-- heading -->
    <header>
      <img src="./assets/pinia-logo.svg">
      <h1>Pinia Tasks2</h1>
    </header>

    <!-- New Task Form -->

    <div class="new-task-form">
      <task-form/>
    </div>

    <!-- filter -->

    <nav class="filter">
      <button @click="filter='all'">All</button>
      <button :class="{favs : filter==='favs'}" @click="filter='favs'">Favorite</button>
    </nav>

    <!-- loading -->

    <div class="loading" v-if="loading">Loading Tasks....</div>

    <!-- task list -->

    <div class="task-list" v-if="filter==='all'">
      <p>You have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>

        <!-- fav task list -->

        <div class="task-list" v-if="filter==='favs'">
      <p>You have {{ favCount }} favorite tasks left to do</p>
      <div v-for="task in favs" :key="task.id">
        <TaskDetails :task="task"/>
      </div>
    </div>

  </main>
</template>

<script>
import { ref } from 'vue';
import TaskForm from './components/TaskForm.vue'
import { useTaskStore } from './stores/TaskStore';
import { storeToRefs } from 'pinia';
import TaskDetails from './components/TaskDetails.vue';
export default {
  components: { TaskForm, TaskDetails },
  setup(){
    const TaskStore = useTaskStore();

    const {tasks, favs, totalCount, favCount, loading} = storeToRefs(TaskStore);

    // fetch tasks

    TaskStore.getTasks();

    const filter = ref('all');

    return {filter, tasks, favs, totalCount, favCount, loading};
  }

}
</script>

<style>

</style>