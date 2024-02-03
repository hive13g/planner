<template>
  <div class="planner-container">
    <div class="lecture-list-container">
      <div class="lecture-list">
        <div
          v-for="lecture in lectures"
          :key="lecture.id"
          class="lecture-item"
          :style="{ backgroundColor: lecture.color }"
        >
          <h3>{{ lecture.title }}</h3>
          <p>Professor: {{ lecture.professor }}</p>
          <p>Time: {{ lecture.time }}</p>
          <!-- Add more details as needed -->
        </div>
      </div>
    </div>
    <div class="calendar-container">
      <FullCalendar :options="calendarOptions" />
    </div>
  </div>
</template>

<script>
import FullCalendar from '@fullcalendar/vue3';
import dayGridPlugin from '@fullcalendar/daygrid';

export default {
  components: {
    FullCalendar
  },
  data() {
    return {
      lectures: Array.from({ length: 10 }, (_, index) => ({
        id: index + 1,
        title: `Lecture ${index + 1}`,
        professor: `Professor ${index + 1}`,
        time: `${8 + index}:00 AM`,
        color: `hsl(${index * 30}, 70%, 80%)`
      })),
      calendarOptions: {
        plugins: [ dayGridPlugin, timeGridPlugin ], // Include the timeGrid plugin
        initialView: 'timeGridWeek', // Set the initial view to timeGridWeek for weekly view
        // Add more options as needed
      }
    };
  }
};
</script>

<style>
.planner-container {
  display: flex;
}

.lecture-list-container {
  width: 20%; /* Adjust the width as needed */
  height: 90vh; /* Set the desired height for the lecture list */
  overflow-y: auto; /* Enable vertical scrolling */
  padding: 20px;
}

.lecture-list {
  display: flex;
  flex-direction: column;
  gap: 10px; /* Add spacing between lecture items */
}

.lecture-item {
  padding: 20px;
  border-radius: 8px;
  /* Additional styles for the lecture items */
}

.calendar-container {
  flex: 1; /* Allow the calendar to fill the remaining space */
  padding: 20px;
}
</style>
