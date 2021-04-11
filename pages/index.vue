<template>
  <div>
    <h1>Events</h1>

    <EventCard
      v-for="(event, index) in events"
      :key="event.id"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
import EventService from '@/services/EventService.js'

export default {
  components: {
    EventCard,
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
  /**
   * context
   *
   * https://nuxtjs.org/docs/2.x/concepts/context-helpers
   */
  async asyncData({ error }) {
    try {
      const { data: events } = await EventService.getEvents()

      return {
        events,
      }
    } catch (err) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events at this time. Please try again.',
      })
    }
  },
}
</script>
