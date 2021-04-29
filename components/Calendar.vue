<template>
  <FullCalendar :options="calendarOptions" />
</template>

<script>
import FullCalendar from '@fullcalendar/vue'
import timeGridPlugin from '@fullcalendar/timegrid'
import interactionPlugin from '@fullcalendar/interaction'
import jaLocale from '@fullcalendar/core/locales/ja'

export default {
  components: {
    FullCalendar,
  },
  data() {
    return {
      calendarOptions: {
        plugins: [timeGridPlugin, interactionPlugin],
        initialView: 'timeGridWeek',
        locale: jaLocale,
        // nowIndicator: true,
        editable: true,
        headerToolbar: {
          left: 'today prev,next title',
          center: '',
          right: '',
        },
        scrollTime: '0:00:00',
        titleFormat: { year: 'numeric', month: 'short' },
        dayHeaderFormat: { day: 'numeric', weekday: 'short' },
        allDaySlot: false, // 終日を非表示
        slotLabelFormat: { hour: 'numeric', minute: '2-digit' },
        // eventColor: '#ff00ff', // イベントの色を変える
        // slotDuration: '00:10:00', // 時間の間隔
        // slotLabelInterval: '00:10:00', // 時間のラベルの間隔
        // slotMinTime: '12:00:00',
        // slotMaxTime: '20:00:00',
        eventColor: 'transparent',
        eventBorderColor: '#FF525C',
        eventTextColor: '#FF525C',
        initialEvents: [
          { title: 'nice event', start: new Date() },
          {
            title: 'Click for Google',
            url: 'http://google.com/',
            start: new Date('2021-04-24'),
          },
        ],
      },
    }
  },
}
</script>

<style>
.fc .fc-today-button,
.fc .fc-today-button:disabled {
  border: 1px solid #333333;
  background: none;
  color: #333333;
  padding-left: 25px;
  padding-right: 25px;
}

.fc .fc-prev-button,
.fc .fc-next-button,
.fc .fc-prev-button:hover,
.fc .fc-next-button:hover,
.fc .fc-prev-button:active,
.fc .fc-next-button:active,
.fc .fc-prev-button:focus,
.fc .fc-next-button:focus {
  background: none !important;
  color: #333333 !important;
  border: none;
  box-shadow: none !important;
}

.fc-toolbar-chunk {
  &:first-child {
    display: flex;
    align-items: center;
  }
}

.fc .fc-toolbar-title {
  font-size: 18px;
}

.fc .fc-timegrid-slot {
  height: 40px;
}
</style>
