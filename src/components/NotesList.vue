<template>
  <div class="mx-auto">
    <v-container fluid>
      <v-row dense>
        <v-col
          v-for="(note, index) in notes"
          :key="index"
          cols="12" md="3" sm="6"
          fluid
        >
          <v-card color="yellow lighten-2" fluid>
            <v-card-title class="headline" v-text="note.title" />

            <v-spacer></v-spacer>

            <v-card-subtitle v-text="note.description" />

            <v-spacer></v-spacer>

            <v-card-actions class="justify-end">
              <v-tooltip bottom>
                <template v-slot:activator="{ on }">
                  <v-btn icon v-on="on">
                    <v-icon>mdi-pencil</v-icon>
                  </v-btn>
                </template>
                <span>Editar</span>
              </v-tooltip>
              <v-tooltip bottom>
                <template v-slot:activator="{ on }">
                  <v-btn icon v-on="on">
                    <v-icon>mdi-delete</v-icon>
                  </v-btn>
                </template>
                <span>Deletar</span>
              </v-tooltip>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </v-container>

    <v-container>
      <v-row>
        <v-col>
          <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
            <template v-slot:activator="{ on }">
              <v-btn
                dark v-on="on"
                fixed
                class="mx-2"
                fab
                dark
                bottom
                right
                color="purple"
              >
                <v-icon dark>mdi-plus</v-icon>
              </v-btn>
            </template>
            <v-card>
              <v-toolbar dark color="yellow darken-1">
                <v-btn icon dark @click="dialog = false">
                  <v-icon>mdi-close</v-icon>
                </v-btn>
                <v-toolbar-title>Settings</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-toolbar-items>
                  <v-btn dark text @click="saveNote">Save</v-btn>
                </v-toolbar-items>
              </v-toolbar>
              <v-form style="margin: 1.7em">
                <v-row>
                  <v-col cols="12">
                    <v-text-field
                      label="Title"
                      v-model="note.title"
                    ></v-text-field>
                    <v-textarea
                      v-model="note.description"
                      name="input-7-4"
                      label="Text note"
                    ></v-textarea>
                  </v-col>
                </v-row>
              </v-form>
            </v-card>
          </v-dialog>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'NotesList',
  data: () => ({
    dialog: false,
    note: {
      title: null,
      description: null
    },
    notes: []
  }),
  methods: {
    saveNote () {
      let note = {}
      note = Object.assign(note, this.note)
      this.notes.push(note)
      this.dialog = false
      this.cleanNote()
    },
    cleanNote () {
      for(let k in this.note) {
        this.note[k] = null
      }
    }
  }
}
</script>
