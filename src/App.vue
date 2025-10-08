<script setup>
import { computed, ref } from 'vue'
const taskName = ref('')
const hideCompleted = ref(false);

const addTask = () => {
  tasks.value.push({
    title: taskName.value,
    completed: false,
    date: Date.now(),
  })
  taskName.value = ''
}

const sortedTask = computed(() => {
  const sortedTask =  tasks.value.toSorted((a,b) => a.completed > b.completed ? 1 : -1 );
  if(hideCompleted.value === true){
    return sortedTask.filter(t => t.completed === false);
  }
  return sortedTask ; 
})

const remainingTask = computed(() => {
  return tasks.value.filter(t => t.completed === false).length;
})

const tasks = ref([
  {
    title:'Task 1',
    completed: false,
    date: 1
  },
  {
    title:'Task 2',
    completed: true,
    date: 2
  }

])
</script>

<template>
  <h1>You did it!</h1>
  <p>Task Management</p>
  <form action="" @submit.prevent="addTask">
    <input type="text" placeholder="New Task" v-model="taskName" />
    <button @click="decrement" :disabled="taskName.length === 0">Add</button>
  </form>
  <!-- <p v-if="count >=5" :style="{color: count >= 5 ? 'red' : 'green' }" >Vous avez cliqué 5 fois </p> -->
  <p v-if="tasks.length === 0">Empty</p>
  <div v-else="tasks.length > 0">
    <ul>
      <li v-for="task in sortedTask" :key="task.date" :class="{completed: task.completed }"> 
      <label for="">
        <input type="checkbox" v-model="task.completed">
        {{ task.title }}
      </label>
      </li>
    </ul>
    <label for="">
      <input type="checkbox" v-model="hideCompleted">
      Hide completed task ?
    </label>
    <p v-if="remainingTask > 0">{{ remainingTask }} tache{{ remainingTask > 1 ? 's' : '' }} à faire</p>
  </div>
</template>

<style scoped>
  .completed{
    text-decoration: line-through;
  }
</style>
