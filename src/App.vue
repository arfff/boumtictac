<template>
  <v-app>
    <v-app-bar app
               color="white"
               flat
               dense>
      <div class="d-flex align-center display-1">
        Boum tic tac
      </div>

      <v-spacer></v-spacer>

      <v-btn href="https://github.com/vuetifyjs/vuetify/releases/latest"
             target="_blank"
             text
             icon>
        <v-icon>mdi-cog</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Bomb />
    </v-main>
  </v-app>
</template>

<script>
import Bomb from './components/Bomb.vue';

export default {
  name: 'App',

  components: {
    Bomb,
  },

  data: () => ({
    //
  }),
};
</script>
