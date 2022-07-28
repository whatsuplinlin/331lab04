<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.dat }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
</template>

<script>
import EventService from '@/services/EventService.js'
import { watchEffect } from '@vue/runtime-core'
export default {
  props: ['id'],
  data() {
    return {
      event: null
    }
  },
  created() {
    watchEffect(() => {
      EventService.getEvents(2, this.page)
        .then((response) => {
          this.events = response.data
        })
        .catch((error) => {
          console.log(error)
        })
    })
  }
}
</script>
