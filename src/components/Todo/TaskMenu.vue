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
    <DialogEdit
      v-if="dialogs.edit"
      :task="task"
      @close="dialogs.edit = false"
    />
    <DialogDueDate
      v-if="dialogs.dueDate"
      :task="task"
      @close="dialogs.dueDate = false"
    />
  </div>
</template>

<script>
import DialogDelete from '../Dialogs/DialogDelete.vue';
import DialogEdit from '../Dialogs/DialogEdit.vue';
import DialogDueDate from '../Dialogs/DialogDueDate.vue';
export default {
  components: { DialogDelete, DialogEdit, DialogDueDate },
  data: () => ({
    items: [
      {
        title: 'Edit',
        icon: 'mdi-pencil',
        click() {
          console.log('edit');
          this.dialogs.edit = true;
        },
      },
      {
        title: 'Due Date',
        icon: 'mdi-calendar',
        click() {
          this.dialogs.dueDate = true;
        },
      },
      {
        title: 'Delete',
        icon: 'mdi-delete',
        click() {
          this.dialogs.delete = true;
        },
      },
      {
        title: 'Sort',
        icon: 'mdi-drag-horizontal-variant',
        click() {
          this.$store.commit('toggleSorting');
        },
      },
    ],
    dialogs: {
      delete: false,
      edit: false,
      dueDate: false,
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
