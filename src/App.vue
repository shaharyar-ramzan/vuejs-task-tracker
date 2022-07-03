<template>
  <div class="container">
    <Header
      @toggle-add-task="toggleAddTask"
      :btnText="toggleAddTask ? 'Add Task' : 'Close'"
      :btnColor="toggleAddTask ? 'green' : 'red'"
      title="Task Tracker"
    />

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
  </div>
</template>

<script>
import Header from "./components/Header.vue"
import Tasks from "./components/Tasks.vue"
import AddTask from "./components/AddTask.vue"

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
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
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
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

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
