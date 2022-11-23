<template>
  <div >
    <h1>{{ message }}</h1>
    <h1>{{ count }}</h1>
    <button @click="countUp">Hochzählen</button>
  </div>
</template>

<script>
export default {
  name: 'TodoApp',
  data() {
    return {
      message: "Hello World",
      count: 0,
    }
  },
  methods: {
    countUp() {
      this.count++;
    },
  },
}
</script>

