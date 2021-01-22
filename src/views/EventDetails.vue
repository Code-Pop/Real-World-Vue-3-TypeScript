<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { EventItem } from '../types'
import EventService from '../services/EventService'
export default defineComponent({
  props: {
    id: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      event: {} as EventItem
    }
  },
  created() {
    EventService.getEvent(this.id)
      .then(response => {
        this.event = response.data
      })
      .catch(error => {
        console.log(error)
      })
  }
})
</script>
