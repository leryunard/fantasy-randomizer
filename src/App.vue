<template>
  <v-app>
    <v-app-bar app color="#3949AB" dark>
      <div class="d-flex align-center">
        <v-img alt="Vuetify Logo" class="shrink mr-2" contain src="https://i.ibb.co/CwmBxCx/fantasy.png"
          transition="scale-transition" width="350" />

      </div>


      <v-spacer></v-spacer>
      <v-btn href="https://github.com/leryunard" target="_blank" text>
        <span class="mr-2">About me</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <FantasyRandomizer />
    </v-main>
  </v-app>
</template>

<script>
import FantasyRandomizer from './components/FantasyRandomizer'

export default {
  name: 'App',

  components: {
    FantasyRandomizer,
  }
}
</script>
