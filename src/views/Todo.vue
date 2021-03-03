<script lang="ts">
import { defineComponent } from 'vue'
import { TodoItem } from '../types'

export default defineComponent({
  data: () => ({
    newTask: {
      label: '',
      type: 'personal'
    } as TodoItem,
    taskItems: [] as TodoItem[]
  }),
  methods: {
    addTask() {
      this.taskItems.push({
        ...this.newTask,
        isComplete: false
      })
    }
  }
})
</script>

<template>
  <h1>Todo</h1>
  <form @submit.prevent>
    <div class="mb1">
      <label for="task-label">Task Label: </label>
      <input type="text" id="task-label" v-model="newTask.label" />
    </div>
    <div>
      <label for="task-type">Take Type: </label>
      <select name="task-type" id="task-type" v-model="newTask.type">
        <option value="personal">Personal</option>
        <option value="work">Work</option>
        <option value="miscellaneous">Miscellaneous</option>
      </select>
    </div>
    <button @click="addTask">Add Task</button>
  </form>
  <h2>Task List</h2>
  <ul>
    <li v-for="(task, index) in taskItems" :key="`task-${index}`">
      {{ task }}
    </li>
  </ul>
</template>

<style scoped>
.mb1 {
  margin-bottom: 1rem;
}
</style>
