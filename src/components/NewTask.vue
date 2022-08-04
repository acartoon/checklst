<template>
  <div>
    <form
      :class="$style.wrapper"
      @submit.prevent="submit"
    >
      <b-form-input
          :class="$style.input"
          v-model="task">

      </b-form-input>
      <b-button
          :disabled="!task"
          type="submit">добавить
      </b-button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: '',
    }
  },
  methods: {
    submit() {
      if(!this.task.length) return;
      this.$emit('addTask', this.task);
      this.task = '';
    }
  }
}
</script>

<style scoped module>
.wrapper {
  display: flex;
  gap: 15px;
  justify-content: center;
}

.input {
  max-width: 350px;
  width: 100%;
}

</style>