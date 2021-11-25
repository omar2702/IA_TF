<template>
  <v-app>
    <v-app-bar
      app
      color="black"
      dark
    >
      <div class="d-flex align-center">
        <h2 class="title">
          Verificador de firmas falsas
        </h2>
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/omar2702/IA_TF/tree/develop"
        target="_blank"
        text
      >
        <span class="mr-2">Repositorio github</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Home/>
    </v-main>
  </v-app>
</template>

<script>
import Home from './components/Home';

export default {
  name: 'App',

  components: {
    Home,
  },

  data: () => ({
    //
  }),
};
</script>
