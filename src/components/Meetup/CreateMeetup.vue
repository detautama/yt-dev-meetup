<template>
  <v-container>
    <v-layout row>
      <v-flex xs12 sm6 offset-sm3>
        <h4>Create Meetup</h4>
      </v-flex>
    </v-layout>
    <v-layout row>
      <v-flex xs12>
        <form @submit.prevent="onCreateMeetup">
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field name="title" label="title" id="title" v-model="title" required></v-text-field>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field name="location" label="Location" id="location" v-model="location" required></v-text-field>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field name="imageUrl" label="Image Url" id="imageUrl" v-model="imageUrl" required></v-text-field>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <img :src="imageUrl" height="150">
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12 sm6 offset-sm3>
              <v-text-field name="desc" label="Description" id="desc" v-model="desc" required></v-text-field>
            </v-flex>
          </v-layout>
          <v-layout>
             <v-flex xs12 sm6 offset-sm3>
              <v-menu
                lazy
                :close-on-content-click="false"
                v-model="menu"
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
                  v-model="date"
                  prepend-icon="event"
                  readonly
                  required
                ></v-text-field>
                <v-date-picker v-model="date" autosave></v-date-picker>
              </v-menu>
            </v-flex>
          </v-layout>
          <v-layout row wrap>
            <v-flex xs12 sm6 offset-sm3>
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
                v-model="time">
                </v-text-field>
                <v-time-picker v-model="time" autosave></v-time-picker>
              </v-menu>
            </v-flex>
          </v-layout>
          <v-layout>
            <v-flex xs12 sm6 offset-sm3>
              <v-btn type="submit">
                Create Meetup
              </v-btn>
            </v-flex>
          </v-layout>
        </form>
      </v-flex>
    </v-layout>
  </v-container>
</template>
<script>
  export default {
    data () {
      return {
        title: '',
        location: '',
        imageUrl: '',
        desc: '',
        date: '',
        time: '',
        menu: false,
        time_menu: false
      }
    },
    computed: {
      formIsValid () {
        return this.title !== '' &&
          this.location !== '' &&
          this.imageUrl !== '' &&
          this.desc !== '' &&
          this.date !== '' &&
          this.time !== ''
      }
    },
    methods: {
      onCreateMeetup () {
        if (!this.formIsValid) {
          return
        }
        const meetupData = {
          title: this.title,
          location: this.location,
          imageUrl: this.imageUrl,
          desc: this.desc,
          date: this.date,
          time: this.time
        }
        this.$store.dispatch('createMeetup', meetupData)
        this.$router.push('/meetups')
      }
    }
  }
</script>