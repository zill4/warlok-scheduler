<template>
  <v-container fill-height fluid>
    <v-row class="text-center" align="center" justify="center">
      <v-col class="mb-5" cols="12">
        <h2 class="headline font-weight-bold mb-3">
          Build a (Smart) Stream Schedule
        </h2>

        <v-row no-gutters align="center" justify="center">
          <v-col sm="2" cols="8">
            <v-card class="pa-2" outlined tile>
              <v-autocomplete
                v-model="values"
                :items="items"
                outlined
                dense
                label="Category"
              ></v-autocomplete>
            </v-card>
          </v-col>
          <v-col sm="1" cols="4">
            <v-card class="pa-2" outlined tile>
              <v-text-field
                v-model="stime"
                label="Start Time"
                value="12:30:00"
                type="time"
                suffix="PST"
              ></v-text-field>
            </v-card>
          </v-col>
          <v-col sm="1" cols="4">
            <v-card class="pa-2" outlined tile>
              <v-text-field
                v-model="etime"
                label="End Time"
                value="12:30:00"
                type="time"
                suffix="PST"
              ></v-text-field>
            </v-card>
          </v-col>
          <v-col sm="2" cols="8">
            <v-card 
            
            class="pa-2" outlined tile>
                    <v-menu
        v-model="menu2"
        :close-on-content-click="false"
        :nudge-right="40"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="date"
            label="Date"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="date"
          @input="menu2 = false"
        ></v-date-picker>
      </v-menu>
            </v-card>
          </v-col>
            <div class="px-10">
                  <v-btn v-on:click='createCal' elevation="4"> Submit </v-btn>
            </div>
        </v-row>
      </v-col>

      <v-col class="mb-5" cols="12">
        <div v-if="show">
         {{schedule}} 
         </div>
        </v-col>
    </v-row>
  </v-container>
</template>

<script>
// var example2 = new Vue({
//   el: '#example-2',
//   data: {
//     name: 'Vue.js'
//   },
//   methods: {
//     greet: function (event) {
//       alert('Hello ' + this.name + '!')
//       if (event) {
//         alert (event.target.tagName)
//       }
//     }
//   }
// })
export default {
  name: "Home",
  methods: {
    greet: function (event) {
      alert("Hello " + this.name + "!");
      if (event) {
        alert(event.target.tagName);
      }
    },
    createCal: function () {
      this.schedule = {
        category: this.values,
        startTime: this.stime,
        endTime: this.etime,
        date: this.date
      }
      this.show = true
    }
  },
  data: () => ({
        items: ['Just Chatting', 'World of Warcraft', 'Final Fantasy VII', 'Black Desert'],
      values: [],
      value: null,
      date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
      menu2: false,
      stime: '01:00',
      etime: '13:00',
      schedule: {},
      show: false
  }),
  // data: () => ({
  //   ecosystem: [
  //     {
  //       text: 'vuetify-loader',
  //       href: 'https://github.com/vuetifyjs/vuetify-loader',
  //     },
  //     {
  //       text: 'github',
  //       href: 'https://github.com/vuetifyjs/vuetify',
  //     },
  //     {
  //       text: 'awesome-vuetify',
  //       href: 'https://github.com/vuetifyjs/awesome-vuetify',
  //     },
  //   ],
  //   importantLinks: [
  //     {
  //       text: 'Documentation',
  //       href: 'https://vuetifyjs.com',
  //     },
  //     {
  //       text: 'Chat',
  //       href: 'https://community.vuetifyjs.com',
  //     },
  //     {
  //       text: 'Made with Vuetify',
  //       href: 'https://madewithvuejs.com/vuetify',
  //     },
  //     {
  //       text: 'Twitter',
  //       href: 'https://twitter.com/vuetifyjs',
  //     },
  //     {
  //       text: 'Articles',
  //       href: 'https://medium.com/vuetify',
  //     },
  //   ],
  //   whatsNext: [
  //     {
  //       text: 'Explore components',
  //       href: 'https://vuetifyjs.com/components/api-explorer',
  //     },
  //     {
  //       text: 'Select a layout',
  //       href: 'https://vuetifyjs.com/getting-started/pre-made-layouts',
  //     },
  //     {
  //       text: 'Frequently Asked Questions',
  //       href: 'https://vuetifyjs.com/getting-started/frequently-asked-questions',
  //     },
  //   ],
  // }),
};
</script>
