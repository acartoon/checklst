<template>
  <div>
    <b-list-group>
      <b-list-group-item :class="[$style.item, {
        [$style.completed]: task.completed,
        [$style.removed]: task.removed,
      }]"
          :key="task.id"
           @click="click(task)"
           v-for="task in tasks">
        <b-form-checkbox
            v-if="!task.completed"
            :class="$style.checkbox"
            type="checkbox" :value="task.completed"
        />
        <span>
          {{task.name}}
        </span>
        <icon-delete
            :class="$style.icon"
          @click.stop="$emit('delete', task.id)"
        />
      </b-list-group-item>
    </b-list-group>

  </div>
</template>

<script>
import IconDelete from "@/components/IconDelete";
export default {
  components: {IconDelete},
  props: {
    tasks: {
      type: Array,
      required: true,
    }
  },
  methods: {
    click(task) {
      console.log(task)
      if(!task.completed) {
        this.$emit('completed', task.id)
      }
    }
  },
  emits: ['completed']
}
</script>

<style module>

.checkbox {
  margin-right: 20px;
}

.item {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.icon {
  margin-left: auto;
  width: 20px;
  height: 20px;
}

.completed {
  background: gray;
}

.removed {
  background: #9c0f0f;
}
</style>