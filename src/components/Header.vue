<template>
  <header class="header">
    <h1>{{ title }}</h1>
    <Button
      v-show="homePage"
      @btn-click-event="$emit('toggle-add-task')"
      :text="btnText"
      :color="btnColor"
    />
  </header>
</template>

<script>
import Button from "./Button.vue"
export default {
  name: "Header",
  //props: ['title']
  props: {
    //title: String,
    title: {
      type: String,
      default: "Hello World",
    },
    btnText: {
      type: String,
      default: "Add Task",
    },
    btnColor: {
      type: String,
      default: "green",
    },
  },
  components: {
    Button,
  },
  computed: {
    homePage() {
      if (this.$route.path === "/") {
        return true
      } else {
        return false
      }
    },
  },
}
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
