<template>
  <div>
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
            <v-icon @click.stop="dialogs.delete = true" color="red"
              >mdi-delete</v-icon
            >
          </v-btn>
        </v-list-item-action>
      </template>
    </v-list-item>
    <v-divider></v-divider>
    <DialogDelete
      v-if="dialogs.delete"
      :task="task"
      @close="dialogs.delete = false"
    />
  </div>
</template>

<script>
import DialogDelete from "../Dialogs/DialogDelete.vue";
export default {
  data() {
    return {
      dialogs: {
        delete: false,
      },
    };
  },
  props: {
    task: {
      type: Object,
      required: false,
    },
  },
  components: { DialogDelete },
};
</script>
