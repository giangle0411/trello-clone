<template >
  <div @click="goToTask(task)">
    <AppDrop @drop="moveTaskOrColumn">
      <AppDrag
        class="task"
        :transferData="{
          type: 'task',
          fromColumnIndex: columnIndex,
          fromTaskIndex: taskIndex
        }"
      >
        <span class="w-full flex-no-shrink font-bold">
          {{ task.name }}
        </span>
        <p v-if="task.description" class="w-full flex-no-shrink mt-1 text-sm">
          {{ task.description }}
        </p>
      </AppDrag>
    </AppDrop>
  </div>
</template>

<script>
import movingTasksColumnsMixin from '@/mixins/movingTasksColumnsMixin'
import AppDrag from '@/components/AppDrag.vue'
import AppDrop from '@/components/AppDrop.vue'

export default {
  components: {
    AppDrag,
    AppDrop
  },
  mixins: [movingTasksColumnsMixin],
  props: {
    task: {
      type: Object,
      required: true
    },
    taskIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    goToTask(task) {
      this.$router.push({ name: 'task', params: { id: task.id } })
    }
  }
}
</script>

<style lang="postcss" scoped>
.task {
  @apply flex items-center flex-wrap shadow mb-2 py-2 px-2 rounded bg-white text-grey-darkest no-underline;
}
</style>
