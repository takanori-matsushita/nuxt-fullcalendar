<template>
  <FullCalendar :options="calendarOptions" />
</template>

<script>
import FullCalendar from '@fullcalendar/vue'
// import dayGridPlugin from '@fullcalendar/daygrid'
import timeGridPlugin from '@fullcalendar/timegrid'
import interactionPlugin from '@fullcalendar/interaction'
export default {
  components: {
    FullCalendar,
  },
  data() {
    return {
      calendarOptions: {
        plugins: [timeGridPlugin, interactionPlugin],
        // initialView: 'timeGridWeek',
      },
    }
  },
}
</script>

<style>
/* @import '~/node_modules/@fullcalendar/common/main.css'; */
/* @import '~/node_modules/@fullcalendar/daygrid/main.css'; */
/* @import '~/node_modules/@fullcalendar/timegrid/main.css'; */
</style>
