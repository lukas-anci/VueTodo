<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" :mobile-breakpoint="768" app>
      <v-img
        class="pa-4 pt-7"
        src="../src/assets/mountains.jpeg"
        height="170"
        gradient="to top right, rgba(19,84,122,.9), rgba(128,208,199,.9)"
      >
        <v-avatar size="70" class="mb-2">
          <img src="../src/assets/avatar.jpg" alt="Lukas" />
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">Bla</div>
        <div class="white--text text-subtitle-2">Bla_bla</div>
      </v-img>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="primary"
      dark
      src="mountains.jpg"
      prominent
      :height="$route.path === '/' ? '238' : '170'"
    >
      <template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
        ></v-img>
      </template>

      <v-container class="header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>
          <v-toolbar-title class="text-h4 ml-4">{{
            $store.state.appTitle
          }}</v-toolbar-title>
        </v-row>
        <v-row> <LiveDateTime /> </v-row>
        <v-row v-if="$route.path === '/'"> <FieldAddTask /> </v-row>
      </v-container>
    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>

<script>
import Snackbar from './components/Global/Snackbar.vue';
import Search from './components/Tools/Search.vue';
import LiveDateTime from './components/Tools/LiveDateTime.vue';
import FieldAddTask from './components/Todo/FieldAddTask.vue';
export default {
  data: () => ({
    drawer: null,
    items: [
      { title: 'Todo', icon: 'mdi-format-list-checks', to: '/' },
      { title: 'About', icon: 'mdi-help-box', to: '/about' },
    ],
  }),
  mounted() {
    this.$store.dispatch('getTasks');
  },
  components: { Snackbar, Search, LiveDateTime, FieldAddTask },
};
</script>
<style lang="sass">
.header-container
   max-width: none
</style>
