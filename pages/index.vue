<script setup lang="ts">
import '@mobiscroll/vue/dist/css/mobiscroll.min.css'
import { MbscDraggable, MbscEventcalendar, type MbscEventcalendarOptions } from '@mobiscroll/vue'
import { useSortable } from '@vueuse/integrations/useSortable'

const options: MbscEventcalendarOptions = {
  dragToMove: true,
  dragToResize: true,
  eventDelete: true,
  externalDrop: true,
  showControls: false,
  theme: 'ios',
  themeVariant: 'dark',
  view: { schedule: { type: 'day', days: false } },
}

const tasks = ref([
  { id: 1, title: 'task a' },
  { id: 2, title: 'task b' },
  { id: 3, title: 'task c' },
  { id: 4, title: 'task d' },
])

const container = ref(null)
const taskElements = ref([])

useSortable(container, tasks)

const draggableToCalendar = true
</script>

<template>
  <div class="flex">
    <div
      ref="container"
      class="grow p-20 space-y-1"
    >
      <div
        v-for="(task, i) in tasks"
        ref="taskElements"
        :key="task.id"
        class="cursor-move border rounded px-2 py-1"
      >
        {{ task.title }}

        <MbscDraggable
          v-if="draggableToCalendar"
          :drag-data="task"
          :element="taskElements[i]"
        />
      </div>
    </div>

    <div class="w-80">
      <MbscEventcalendar
        v-bind="options"
      />
    </div>
  </div>
</template>
