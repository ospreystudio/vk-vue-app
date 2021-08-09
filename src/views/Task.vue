<template>
<div class="row">
  <div v-if="task" class="col s6 offset-s3">
  <h1> {{ task.title }} </h1>

  <form @submit.prevent="submitHandler">
    <div class="chips" ref="chips"></div>
    <div class="input-field">
      <textarea style="min-height: 150px" id="description" class="materialize-textarea" v-model="description"></textarea>
      <label for="description">Description</label>
      <span class="character-counter" style="font-size: 12px; float: right">{{description.length}}/2048</span>
    </div>
    <input type="text" ref="datepicker">
    <button class="btn" type="submit"> Create task </button>
  </form>
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
  data: () => ({
    description: '',
    chips: null,
    date: null
  }),
  mounted() {
    this.description = this.task.description
    this.chips = M.Chips.init(this.$refs.chips, {
      placeholder: 'Task tags',
      data: this.task.tags
    })
    this.date = M.Datepicker.init(this.$refs.datepicker, {
      format: 'dd.mm.yyyy',
      defaultDate: new Date(),
      setDefaultDate: true
    })
    setTimeout(() => {
      M.updateTextFields()
    }, 0)
  },
  methods: {
    submitHandler() {
      this.$store.dispatch('createTask', task)
      this.$router.push('/list')
    }
  },
  destroyed() {
    if (this.date && this.date.destroy) {
      this.date.destroy()
    }
    if (this.chips && this.chips.destroy) {
      this.chips.destroy()
    }
  }
}
</script>

<style scoped>

</style>