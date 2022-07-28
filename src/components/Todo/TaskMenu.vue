<template>
  <div>
    <v-menu bottom left>
      <template v-slot:activator="{ on, attrs }">
        <v-btn icon v-bind="attrs" v-on="on">
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
      </template>

      <v-list>
        <v-list-item
          @click="handleClick(i)"
          v-for="(item, i) in items"
          :key="i"
        >
          <v-list-item-title>{{ item.title }}</v-list-item-title>
          <v-list-item-icon>
            <v-icon v-text="item.icon"></v-icon>
          </v-list-item-icon>
        </v-list-item>
      </v-list>
    </v-menu>
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
  components: { DialogDelete },
  data: () => ({
    items: [
      {
        title: "Edit",
        icon: "mdi-pencil",
        click() {
          console.log("edit");
        },
      },
      {
        title: "Due Date",
        icon: "mdi-calendar",
        click() {
          console.log("edit");
        },
      },
      {
        title: "Delete",
        icon: "mdi-delete",
        click() {
          this.dialogs.delete = true;
        },
      },
    ],
    dialogs: {
      delete: false,
    },
  }),
  methods: {
    handleClick(i) {
      this.items[i].click.call(this);
    },
  },
  props: {
    task: {
      required: false,
    },
  },
};
</script>

<style></style>
