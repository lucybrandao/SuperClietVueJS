<template>
  <v-card color="yellow lighten-2" fluid>
    <v-card-title class="headline" v-text="note.title" />
      <!-- <v-spacer /> -->
    <v-card-subtitle v-text="note.description" />

    <v-spacer></v-spacer>

    <v-card-actions class="justify-end">
      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on" @click="$emit('clickEditNote', id)">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
        </template>
        <span>Editar</span>
      </v-tooltip>
      <v-tooltip bottom>
        <template v-slot:activator="{ on }">
          <v-btn icon v-on="on"  @click="$emit('clickRemoveNote', id)">
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </template>
        <span>Deletar</span>
      </v-tooltip>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: 'CardNote',
  props: {
    note: Object,
    id: Number
  }
}
</script>
