<template>
  <v-app>
    <v-app-bar
      app
      color="purple darken-2"
      dark
    >
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-spacer></v-spacer>
      
      <v-btn target="_blank" text>
        <span class="mr-2">My Notes</span>
      </v-btn>
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
