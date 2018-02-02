<template>
  <v-app>
    <v-toolbar>
      <v-toolbar-side-icon 
      @click.stop="sideNav = !sideNav"></v-toolbar-side-icon>
    </v-toolbar>
    <main>
      <v-container>
        <v-layout row wrap>
          <v-flex xs12>Tes</v-flex>
        </v-layout>
      </v-container>
    </main>
    <v-navigation-drawer absolute temporary v-model="sideNav">
      <v-list>
        <v-list-tile>
          <v-list-tile-action>
            <v-icon>person</v-icon>
          </v-list-tile-action>
          <v-list-tile-content class="grey--text text-darken-1">
            User
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
  </v-app>
</template>

<script>
  export default {
    data () {
      return {
        sideNav: false
      }
    },
    name: 'App'
  }
</script>
