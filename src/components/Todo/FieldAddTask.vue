<template>
  <v-text-field
    v-model="newTaskTitle"
    class="field-add-task pa-3"
    outlined
    placeholder="Add Task"
    hide-details
    clearable
    @keyup.enter="addTask"
  >
    <template v-slot:append>
      <v-icon :disabled="newTaskTitleInvalid" color="primary" @click="addTask"
        >mdi-plus</v-icon
      >
    </template></v-text-field
  >
</template>

<script>
export default {
  data() {
    return {
      newTaskTitle: '',
    };
  },
  computed: {
    newTaskTitleInvalid() {
      return !this.newTaskTitle;
    },
  },
  methods: {
    addTask() {
      if (!this.newTaskTitleInvalid) {
        this.$store.dispatch('addTask', this.newTaskTitle);
        this.newTaskTitle = '';
      }
    },
  },
};
</script>
