<template>
  <v-app>
    <v-app-bar
      app
      color="purple darken-2"
      dark
    >
      <v-spacer></v-spacer>

      <v-tooldbar-title class="headline thin">
        KEEP VIEW
      </v-tooldbar-title>

      <v-spacer></v-spacer>

    </v-app-bar>

    <v-content>
      <NotesList/>
    </v-content>

  </v-app>
</template>

<script>
import NotesList from './components/NotesList'

export default {
  name: 'App',

  components: {
    NotesList
  },

  data: () => ({
    //
  })
}
</script>
