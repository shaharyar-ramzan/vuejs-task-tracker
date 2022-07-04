<template>
  <div v-if="showAddTask">
    <AddTask
      @add-task="addTask"
      @update-task="updateTask"
      :updateData="taskData"
    />
  </div>

  <Tasks
    @toggle-reminder="toggleReminder"
    @data-update-task="dataUpdateTask"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from "../components/Tasks.vue"
import AddTask from "../components/AddTask.vue"

export default {
  name: "Home",
  props: {
    showAddTask: Boolean,
  },
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      taskData: {},
    }
  },
  methods: {
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      //console.log(id)
      if (confirm("Are you sure?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    updateTask(data) {
      console.log(data)
      this.tasks = this.tasks.map((task) =>
        task.id === data.id
          ? {
              ...task,
              id: data.id,
              text: data.text,
              day: data.day,
              reminder: data.reminder,
            }
          : task
      )
    },
    dataUpdateTask(task) {
      this.taskData = task
      this.showAddTask = false
      setTimeout(() => {
        this.showAddTask = true
        //console.log("this", this.taskData)
      }, 100)
    },
    toggleReminder(id) {
      //console.log(id)
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      )
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doctors Appointment",
        day: "Feb 5th at 2:30pm",
        reminder: true,
      },
      {
        id: 2,
        text: "Meeting at School",
        day: "Feb 6th at 1:30pm",
        reminder: true,
      },
      {
        id: 3,
        text: "Meeting 2 at School",
        day: "Feb 6th at 2:30pm",
        reminder: false,
      },
    ]
  },
}
</script>
