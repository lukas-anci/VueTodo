<template>
  <div class="home">
    <FieldAddTask />
    <ListTasks v-if="$store.state.tasks.length" />
    <NoTask v-else />
    <ButtonDoneSorting v-if="$store.state.sorting" />
  </div>
</template>

<script>
import FieldAddTask from '../components/Todo/FieldAddTask.vue';
import ListTasks from '../components/Todo/ListTasks.vue';
import NoTask from '../components/Todo/NoTask.vue';
import ButtonDoneSorting from '../components/Todo/ButtonDoneSorting.vue';
// @ is an alias to /src

export default {
  name: 'Home',
  data() {
    return {
      newTaskTitle: '',
    };
  },
  methods: {},
  components: { FieldAddTask, ListTasks, NoTask, ButtonDoneSorting },
};
</script>
