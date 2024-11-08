<template>
  <div class="w-full max-w-md">
    <div class="bg-white rounded-lg shadow p-8 text-center">
      <!-- Date Display -->

      <!-- Calendar -->
      <div class="mb-4">
        <div class="flex justify-between items-center mb-4">
          <button
            @click="previousMonth"
            class="p-1 hover:bg-emerald-100 rounded"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5"
              viewBox="0 0 20 20"
              fill="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
                clip-rule="evenodd"
              />
            </svg>
          </button>
          <span class="text-lg font-semibold"
            >{{ currentMonthName }} {{ currentYear }}</span
          >
          <button @click="nextMonth" class="p-1 hover:bg-emerald-100 rounded">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5"
              viewBox="0 0 20 20"
              fill="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                clip-rule="evenodd"
              />
            </svg>
          </button>
        </div>

        <!-- Days of Week -->
        <div class="grid grid-cols-7 gap-1 mb-2">
          <template v-for="day in daysOfWeek" :key="day">
            <div class="text-center text-gray-600 text-sm">{{ day }}</div>
          </template>
        </div>

        <!-- Calendar Days -->
        <div class="grid grid-cols-7 gap-1">
          <template v-for="day in calendarDays" :key="day.date">
            <button
              @click="selectDate(day.date)"
              :class="[
                'p-2 text-sm rounded-full hover:bg-emerald-100',
                isToday(day.date) ? 'bg-emerald-50' : '',
                isSameDay(day.date, selectedDate)
                  ? 'bg-emerald-500 text-white hover:bg-emerald-600'
                  : '',
                !day.isCurrentMonth ? 'text-gray-400' : '',
              ]"
            >
              {{ day.date.getDate() }}
            </button>
          </template>
        </div>
      </div>

      <!-- Time Picker -->
      <div class="flex space-x-4 justify-center">
        <select
          v-model="selectedHour"
          class="block w-20 rounded-md border-emerald-300 shadow-sm focus:border-emerald-500 focus:ring-emerald-500"
        >
          <option v-for="hour in 24" :key="hour - 1" :value="hour - 1">
            {{ (hour - 1).toString().padStart(2, "0") }}
          </option>
        </select>
        <span class="text-xl">:</span>
        <select
          v-model="selectedMinute"
          class="block w-20 rounded-md border-emerald-300 shadow-sm focus:border-emerald-500 focus:ring-emerald-500"
        >
          <option v-for="minute in 60" :key="minute - 1" :value="minute - 1">
            {{ (minute - 1).toString().padStart(2, "0") }}
          </option>
        </select>
      </div>
      <br />
      <NuxtLink to="details" class="bg-emerald-500 text-white rounded-lg py-2 px-2 w-full">
        <span class="text-lg font-semibold" id="time">{{
          formatDate(selectedDate)
        }}</span>
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import {
  startOfMonth,
  endOfMonth,
  startOfWeek,
  endOfWeek,
  eachDayOfInterval,
  format,
  addMonths,
  subMonths,
  isToday as _isToday,
  isSameDay as _isSameDay,
  getMonth,
  getYear,
  setHours,
  setMinutes,
} from "date-fns";

const selectedDate = ref(new Date());
const currentMonth = ref(new Date());
const selectedHour = ref(new Date().getHours());
const selectedMinute = ref(new Date().getMinutes());

const daysOfWeek = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];

const currentMonthName = computed(() => format(currentMonth.value, "MMMM"));
const currentYear = computed(() => getYear(currentMonth.value));

const calendarDays = computed(() => {
  const start = startOfWeek(startOfMonth(currentMonth.value));
  const end = endOfWeek(endOfMonth(currentMonth.value));

  return eachDayOfInterval({ start, end }).map((date) => ({
    date,
    isCurrentMonth: getMonth(date) === getMonth(currentMonth.value),
  }));
});

const nextMonth = () => {
  currentMonth.value = addMonths(currentMonth.value, 1);
};

const previousMonth = () => {
  currentMonth.value = subMonths(currentMonth.value, 1);
};

const selectDate = (date) => {
  selectedDate.value = setMinutes(
    setHours(date, selectedHour.value),
    selectedMinute.value
  );
};

const formatDate = (date) => {
  return format(date, "MMMM d, yyyy HH:mm");
};

const isToday = (date) => _isToday(date);
const isSameDay = (date1, date2) => _isSameDay(date1, date2);
</script>
