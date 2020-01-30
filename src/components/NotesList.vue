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
          <card-note
            :note="note"
            :id="index"
            @clickEditNote="editNote"
            @clickRemoveNote="removeNote"
          />
        </v-col>
      </v-row>
    </v-container>

    <v-container>
      <v-row>
        <v-col>
          <v-dialog
            v-model="dialog"
            fullscreen
            hide-overlay
            transition="dialog-bottom-transition"
          >
            <template v-slot:activator="{ on }">
              <v-btn
                dark v-on="on"
                fixed
                class="mx-2"
                fab
                bottom
                right
                color="purple"
              >
                <v-icon dark>mdi-plus</v-icon>
              </v-btn>
            </template>
            <v-card>
              <v-toolbar dark color="yellow accent-4">
                <v-btn icon dark @click="dialog = false">
                  <v-icon>mdi-close</v-icon>
                </v-btn>
                <v-toolbar-title>My Note</v-toolbar-title>
                <v-spacer />
                <v-toolbar-items>
                  <v-btn dark text @click="saveNote">Save</v-btn>
                </v-toolbar-items>
              </v-toolbar>
              <v-form 
                style="margin: 1.7em"
                ref="form"
                lazy-validation
              >
                <v-row>
                  <v-col cols="12">
                    <v-text-field
                      label="Title"
                      v-model="note.title"
                      required
                      :rules="titleRule"
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
import CardNote from './CardNote'

export default {
  name: 'NotesList',
  components: {
    CardNote
  },
  data: () => ({
    dialog: false,
    note: {
      title: null,
      description: null
    },
    notes: [],
    titleRule: [
      v => !!v || 'Title is required'
    ]
  }),
  methods: {

    saveNote () {
      let note = {}
      note = Object.assign(note, this.note)
      if (this.$refs.form.validate()) {
        if (note.id !== null && note.id >= 0) {
          this.notes[note.id] = note
        } else {
          this.notes.push(note)
        }
        this.dialog = false
        this.$refs.form.reset()
      }
    },
    editNote (id) {
      this.note = this.notes[id]
      this.note.id = id
      this.dialog = true
    },
    removeNote (id) {
      this.notes.splice(id, 1)
    }
  }
}
</script>
