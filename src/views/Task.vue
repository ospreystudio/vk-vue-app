<template>
<div>
  <div v-if="task">
  <h1> {{ task.title }} </h1>
  </div>
  <p v-else> Task not found </p>
</div>
</template>

<script>


export default {
  name: "Task",
  computed: {
    task() {
      return this.$store.getters.taskById(+this.$route.params.id)
    }
  },
  data() {
    return {

    }
  }
}
</script>

<style scoped>

</style>