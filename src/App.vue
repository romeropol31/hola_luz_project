

<template>
  <v-app>
    <NavBar />

    <v-main>
      <CupSearch />
    </v-main>
  </v-app>
</template>

<script>

import NavBar from './components/NavBar.vue';
import CupSearch from './components/CupSearch.vue';

export default {
  name: 'App',

  components: {
    NavBar,
    CupSearch
  },

  data: () => ({
    //
  }),
};
</script>
