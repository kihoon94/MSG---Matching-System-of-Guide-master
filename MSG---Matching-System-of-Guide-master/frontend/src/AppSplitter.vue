<template>
  <v-ons-page>
    <v-ons-splitter>
      <v-ons-splitter-side swipeable side="right" collapse=""
      width="260px"
      :swipe-target-width="md && 25"
      :animation="md ? 'overlay' : 'reveal'"
      :open.sync="isOpen"
      >
      <div class="type1">
        <menu-page></menu-page>
      </div>
      </v-ons-splitter-side>
      <v-ons-splitter-content>
        <app-tabbar></app-tabbar>
      </v-ons-splitter-content>
    </v-ons-splitter>
  </v-ons-page>
</template>

<script>
import AppTabbar from './AppTabbar.vue';
import MenuPage from './pages/Menu.vue';
import Menu_test from './pages/Menu_test.vue';

export default {
  computed: {
    isOpen: {
        get() {
          return this.$store.state.splitter.open;
        },
        set(newValue) {
          this.$store.commit('splitter/toggle', newValue)
      }
    }
  },
  components: {AppTabbar, MenuPage, Menu_test}
};
</script>

<style>
ons-splitter-side[animation=overlay] {
  border-left: 1px solid #bbb;
}
</style>
