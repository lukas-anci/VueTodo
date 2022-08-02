<template>
  <div class="home">
    <ListTasks v-if="$store.state.tasks.length" />
    <NoTask v-else />
    <ButtonDoneSorting v-if="$store.state.sorting" />
  </div>
</template>

<script>
import ListTasks from '../components/Todo/ListTasks.vue';
import NoTask from '../components/Todo/NoTask.vue';
import ButtonDoneSorting from '../components/Todo/ButtonDoneSorting.vue';

export default {
  name: 'Home',
  data() {
    return {
      newTaskTitle: '',
    };
  },
  methods: {},
  components: { ListTasks, NoTask, ButtonDoneSorting },
};
</script>
