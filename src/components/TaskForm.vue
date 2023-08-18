<template>
  <form @submit.prevent="handleSubmit">
    <input type="text" placeholder="todo" v-model="newTask">
    <button>Add</button>
  </form>
</template>

<script>
import { ref } from 'vue'
import {useTaskStore} from "../stores/TaskStore"
export default {
  setup(){
    const taskStore = useTaskStore();
    const newTask = ref('');
    const handleSubmit = () => {
      if(newTask.value.length>0){
      taskStore.addTask({
        id: Math.floor(Math.random()*10000),
        title: newTask.value,
        isFav: false
      }) // end add task
    } // end if contion
    newTask.value = '';

    } // end handle submit
    
    return {handleSubmit, newTask}
  } // end setup
  
} // end export default
</script>

<style>

</style>