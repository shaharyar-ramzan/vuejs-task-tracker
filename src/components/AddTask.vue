<template>
  <form @submit="onSubmit" class="add-form">
    <div>Update Data = {{ updateData }}</div>
    <div class="form-control">
      <label>Task</label>
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text"
        v-model="day"
        name="day"
        placeholder="Add Day & Time"
      />
    </div>
    <div class="form-control form-control-check">
      <input type="checkbox" v-model="reminder" name="reminder" />
      <label>Set Reminder</label>
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  props: {
    updateData: {
      type: Object,
      default: {},
    },
  },
  data() {
    return {
      text: this.updateData.text ? this.updateData.text : "",
      day: this.updateData.day ? this.updateData.day : "",
      reminder: this.updateData.reminder ? this.updateData.reminder : false,
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()
      if (!this.text) {
        alert("Please add a task")
        return
      }
      const taskData = {
        id: this.updateData.id
          ? this.updateData.id
          : Math.floor(Math.random() * 100000),
        text: this.text,
        day: this.day,
        reminder: this.reminder,
      }
      console.log(this.updateData.id)

      if (this.updateData.id) {
        this.$emit("update-task", taskData)
      } else {
        this.$emit("add-task", taskData)
      }

      this.text = ""
      this.day = ""
      this.reminder = false
    },
  },
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>
