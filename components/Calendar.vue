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
        // dayHeaderFormat: { day: 'numeric' },
        dayHeaderFormat(date) {
          const day = date.date.day
          return day
        },
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
          { title: 'nice event', start: new Date('2021-5-4 10:00:00') },
          {
            title: 'Click for Google',
            url: 'http://google.com/',
            start: new Date('2021-04-24'),
          },
        ],
      },
    }
  },
  mounted() {
    this.pressChangeWeek()
    this.addWeekday()
  },
  methods: {
    pressChangeWeek() {
      const buttons = document.querySelectorAll(
        '.fc-today-button, [aria-label="prev"], [aria-label="next"]'
      )
      for (const btn of buttons) {
        btn.addEventListener('click', () => {
          this.addWeekday()
        })
      }
    },
    addWeekday() {
      const weekdays = document.getElementsByClassName('fc-col-header-cell')
      const weekdaysText = ['日', '月', '火', '水', '木', '金', '土']
      for (let i = 0; i <= 6; i++) {
        const el = document.createElement('span')
        el.className = 'weekday'
        if (weekdays[i].classList.contains('fc-day-today')) {
          el.classList.add('weekday--today')
        }
        el.textContent = weekdaysText[i]
        weekdays[i].prepend(el)
      }
    },
  },
}
</script>

<style>
/* toolbar style */
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

.fc-col-header-cell {
  border-left: none !important;
  border-right: none !important;
}

.fc .fc-scrollgrid-section-header > * {
  border: none;
}

.fc .fc-scrollgrid-section > * {
  border-bottom: none;
}

.fc-timegrid-axis,
.fc-theme-standard .fc-scrollgrid,
.fc .fc-timegrid-slot-label {
  border: none !important;
}

.fc .fc-day {
  font-size: 22px;
}

.fc .fc-day-today {
  position: relative;
  color: #fff;
  /* background: #ff525c; */
}

.fc-col-header,
.fc-col-header-cell {
  height: 50px !important;
}

.weekday {
  color: rgba(0, 0, 0, 0.3);
  font-size: 10px;
}

.weekday--today {
  color: #ff525c;
}

.fc-scrollgrid-sync-inner {
  margin-bottom: 10px;
}

.fc-col-header-cell.fc-day-today:before {
  content: '';
  position: absolute;
  bottom: 11px;
  left: 50%;
  transform: translateX(-50%);
  width: 35px;
  height: 35px;
  background: #ff525c;
  border-radius: 50%;
  z-index: -1;
}
</style>
