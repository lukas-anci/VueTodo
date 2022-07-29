<template>
  <v-dialog :value="true" width="600px">
    <v-card>
      <v-card-title>
        <span class="text-h5">Edit Task</span>
      </v-card-title>
      <v-card-text>
        Edit the title of this task

        <v-text-field
          v-model="taskTitle"
          @keyup.enter="saveTask"
        ></v-text-field>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn text @click="$emit('close')"> Cancel </v-btn>
        <v-btn :disabled="taskTitleInvalid" color="red" text @click="saveTask">
          Save
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  data() {
    return {
      taskTitle: null,
    };
  },
  props: {
    task: {
      type: Object,
    },
  },
  mounted() {
    this.taskTitle = this.task.title;
  },
  computed: {
    taskTitleInvalid() {
      return !this.taskTitle || this.taskTitle === this.task.title;
    },
  },
  methods: {
    saveTask() {
      if (!this.taskTitleInvalid) {
        let payload = {
          id: this.task.id,
          title: this.taskTitle,
        };
        this.$store.dispatch("updateTaskTitle", payload);
        this.$emit("close");
      }
    },
  },
};
</script>

<style></style>
