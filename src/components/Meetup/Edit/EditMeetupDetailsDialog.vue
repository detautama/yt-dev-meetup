<template>
  <v-dialog width="350px" persistent v-model="editDialog">
      <v-btn fab accent slot="activator">
        <v-icon>edit</v-icon>
      </v-btn>
      <v-card>
        <v-container>
          <v-layout row wrap>
            <v-flex xs12>
              <v-card-title>Edit Meetups</v-card-title>
            </v-flex>
          </v-layout>
          <v-divider></v-divider>
          <v-layout row wrap>
            <v-flex xs12>
              <v-card-text>
                <v-text-field
                  name="title"
                  label="title"
                  id="title"
                  v-model="editedTitle"
                  required></v-text-field>
                <v-text-field
                name="description"
                label="Description"
                id="desc"
                multi-line
                v-model="editedDescription"
                required></v-text-field>
              </v-card-text>
            </v-flex>
          </v-layout>
          <v-divider></v-divider>
          <v-layout>
             <v-flex xs12>
              <v-menu
                lazy
                :close-on-content-click="false"
                v-model="date_menu"
                transition="scale-transition"
                offset-y
                full-width
                :nudge-right="40"
                max-width="290px"
                min-width="290px"
              >
                <v-text-field
                  slot="activator"
                  label="Picker in menu"
                  v-model="editedDate"
                  prepend-icon="event"
                  readonly
                  required
                ></v-text-field>
                <v-date-picker v-model="editedDate" autosave></v-date-picker>
              </v-menu>
            </v-flex>
          </v-layout>
          <v-divider></v-divider>
           <v-layout row wrap>
            <v-flex xs12>
              <v-menu
              lazy
              :close-on-content-click="false"
              v-model="time_menu"
              transition="scale-transition"
              offset-y
              full-width
              :nudge-right="40"
              max-width="290px"
              min-width="290px">
                <v-text-field
                slot="activator"
                label="Time"
                prepend-icon="access_time"
                readonly
                v-model="editedTime">
                </v-text-field>
                <v-time-picker v-model="editedTime" autosave></v-time-picker>
              </v-menu>
            </v-flex>
          </v-layout>
          <v-divider></v-divider>
          <v-layout row wrap>
            <v-flex xs12 row wrap>
              <v-card-actions>
                <v-btn
                flat
                class="blue--text darken-1"
                @click="editDialog = false">Close</v-btn>
              <v-btn flat class="blue--text darken-1" @click="onSaveChanges">Save</v-btn>
              </v-card-actions>
            </v-flex>
          </v-layout>
        </v-container>
      </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: ['meetup'],
  data () {
    return {
      editDialog: false,
      editedTitle: this.meetup.title,
      editedDescription: this.meetup.desc,
      editedDate: this.meetup.date,
      editedTime: this.meetup.time,
      date_menu: false,
      time_menu: false
    }
  },
  methods: {
    onSaveChanges () {
      if (this.editedTitle.trim() === '' || this.editedDescription.trim() === '') {
        return
      }
      this.editDialog = false
      this.$store.dispatch('updateMeetupData', {
        id: this.meetup.id,
        title: this.editedTitle,
        desc: this.editedDescription,
        date: this.editedDate,
        time: this.editedTime
      })
    }
  }
}
</script>
