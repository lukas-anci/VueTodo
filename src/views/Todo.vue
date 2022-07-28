<template>
  <div class="home">
    <v-text-field
      v-model="newTaskTitle"
      class="pa-3"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      hide-details
      clearable
      @click:append="addTask"
      @keyup.enter="addTask"
    ></v-text-field>

    <v-list v-if="$store.state.tasks.length" flat class="pt-0">
      <div v-for="task in $store.state.tasks" :key="task.id">
        <v-list-item
          @click="$store.commit('doneTask', task.id)"
          :class="{ green: task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
                >{{ task.title }}</v-list-item-title
              >
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon>
                <v-icon
                  @click.stop="$store.commit('deleteTask', task.id)"
                  color="red"
                  >mdi-delete</v-icon
                >
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>

    <div v-else class="no-tasks">
      <v-icon size="100" color="primary">mdi-check</v-icon>

      <div class="text-h5 primary--text">No tasks</div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  data() {
    return {
      newTaskTitle: "",
    };
  },
  methods: {
    addTask() {
      this.$store.commit("addTask", this.newTaskTitle);
      this.newTaskTitle = "";
    },
  },
};
</script>

<style lang="scss">
.no-tasks {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%);
  opacity: 0.5;
}
</style>
