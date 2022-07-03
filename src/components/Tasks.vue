<template>
  <div :key="task.id" v-for="task in tasks">
    <Task
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @data-update-task="$emit('data-update-task', task)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
  </div>
</template>

<script>
import Task from "./Task"
export default {
  name: "Tasks",
  props: {
    tasks: {
      type: Array,
      default: [],
    },
  },
  components: {
    Task,
  },
}
</script>
