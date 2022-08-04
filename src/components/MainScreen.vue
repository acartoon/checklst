<template>
  <main>
    <b-container>
    <h1 :class="$style.wrapper">Список задач</h1>
    <new-task
      :class="$style.wrapper"
      @add-task="addTask"
    />
    <div>

      <check-list
          @completed="completedTask"
          @delete="removeTask"
          :tasks="taskList"
      />
    </div>
    </b-container>
  </main>
</template>

<script>

import CheckList from "@/components/CheckList";
import NewTask from "@/components/NewTask";

export default {
  components: {
    NewTask,
    CheckList,
  },
  data() {
    return {
      taskList: [],
    }
  },
  computed: {
  },
  methods: {
    addTask(task) {
      const newTask = {
        name: task,
        id:  new Date().getTime(),
        completed: false,
        removed: false,
      }
      this.taskList.push(newTask);
    },

    completedTask(id) {
      const task = this.taskList.find(task => task.id === id);
      if(!task) {
        console.error(`задачи с ${id} не существует!`);
        return;
      }
      if(task.removed) return;
      task.completed = true;
    },

    removeTask(id) {
      const taskIndex = this.taskList.findIndex(task => task.id === id);
      const task = this.taskList.find(task => task.id === id);
      if(taskIndex === -1) {
        console.error(`задачи с ${id} не существует!`);
        return;
      }
      task.removed = true;
      // this.taskList = [...this.taskList.slice(0, taskIndex), ...this.taskList.slice(taskIndex + 1)]
    }
  }
}
</script>

<style module >

.wrapper {
  margin-bottom: 15px;
}
</style>