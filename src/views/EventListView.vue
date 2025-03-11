<script setup>
import EventCard from '@/components/EventCard.vue'
import { onMounted, ref } from 'vue'
import EventService from '@/services/EventService.js'

const events = ref(null)
const fetchData = async () => {
  try {
    const response = await EventService.getEvents()
    events.value = response.data
  } catch (err){
    console.log(err)
  }
}
onMounted(async () => {
  await fetchData()
  console.log(events.value)
})
</script>

<template>
  <h1>Events For Good</h1>
  <div class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event" />
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
