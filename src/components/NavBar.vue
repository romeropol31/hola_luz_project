<template>
    <v-app-bar app color="light-green" dark>
      <div class="d-flex align-center">
        <v-app-bar-nav-icon v-if="$vuetify.breakpoint.mobile" @click="drawer = true"></v-app-bar-nav-icon>
        <v-img
          alt="Vuetify Logo"
          :class="$vuetify.breakpoint.mobile ? null : 'ml-11'"
          src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Logo_de_Holaluz_.png"
          transition="scale-transition"
          width="100"
        />
      </div>
      <div v-if="!$vuetify.breakpoint.mobile" class="mt-2">
        <a class="mr-2 ml-5 white--text">Electricity Rates</a>
        <a class="mr-2 ml-5 white--text">Solar panels</a>
        <a class="mr-2 ml-5 white--text">Companies</a>
        <a class="mr-2 ml-5 white--text">Producers</a>
        <a class="mr-2 ml-5 white--text">Blog</a>
      </div>

      <v-spacer></v-spacer>
        <div v-if="$vuetify.breakpoint.mobile ? false : true" class="mt-1" >
          <v-btn elevation="2" outlined rounded small class="pink ma-2">Contract</v-btn>
          <v-btn elevation="2" outlined rounded small class="pink ma-2">Client Zone</v-btn>
          <span class="mr-2 body-2">100% green light</span>
        </div>
    </v-app-bar>
</template>

<script>
  export default {
    data: () => ({
      drawer: false,
    }),
  }
</script>