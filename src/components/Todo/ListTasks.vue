<template>
  <v-list flat class="pt-0">
    <draggable v-model="tasks" handle=".handle">
      <Task v-for="task in tasks" :key="task.id" :task="task" />
    </draggable>
  </v-list>
</template>

<script>
import draggable from 'vuedraggable';
import Task from './Task.vue';
export default {
  computed: {
    tasks: {
      get() {
        return this.$store.getters.tasksFiltered;
      },
      set(value) {
        this.$store.dispatch('setTasks', value);
      },
    },
  },

  components: { Task, draggable },
};
</script>
