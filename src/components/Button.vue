<template>
  <button
    @click="$emit('btn-click-event')"
    :style="{ background: color }"
    class="btn"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  //props: ['title']
  props: {
    //title: String,
    color: {
      type: String,
      default: "green",
    },
    text: {
      type: String,
      default: "Button",
    },
  },
  /*methods: {
    onClick() {
      console.log('click')
    }
  }*/
}
</script>
