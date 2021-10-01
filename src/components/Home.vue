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
                v-model="value"
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
            <v-card class="pa-2" outlined tile>
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
            <v-btn v-on:click="createCal" elevation="4"> Submit </v-btn>
          </div>
        </v-row>
      </v-col>

      <v-col class="mb-5" cols="12">
        <div v-if="show">
          <v-card class="mx-auto" max-width="1000">
            <v-img
              class="white--text align-end"
              height="200px"
              :src='gameUrl'
            >
              <v-card-title>{{schedule.category}} Stream</v-card-title>
            </v-img>

            <v-card-subtitle class="pb-0"> {{schedule.duration}} hour stream</v-card-subtitle>

            <v-card-text class="text--primary">
              <div>From {{schedule.startTime }} to {{schedule.endTime}}</div>

              <div>{{schedule.date}}</div>
            </v-card-text>
          </v-card>
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
      msToTime: function (duration) {
        var minutes = Math.floor((duration / (1000 * 60)) % 60),
          hours = Math.floor((duration / (1000 * 60 * 60)) % 24)

        hours = (hours < 10) ? "0" + hours : hours
        minutes = (minutes < 10) ? "0" + minutes : minutes

        return hours + ":" + minutes
      },
      getTimeDiff: function (stime, etime) {
      var start = stime.replace(':','')
      var end = etime.replace(':', '')
      var d1 = new Date(0)
      var d2 = new Date(0)

      d1.setHours(parseInt(start.toString().substr(0, 2), 10))
      d1.setMinutes(parseInt(start.toString().substr(2, 2), 10))

      d2.setHours(parseInt(end.toString().substr(0, 2), 10))
      d2.setMinutes(parseInt(end.toString().substr(2, 2), 10))

      return this.msToTime(d2.getTime() - d1.getTime())
    },
    createCal: function () {
      var d = new Date(this.date)
      
      this.schedule = {
        category: this.value,
        startTime: this.stime,
        endTime: this.etime,
        date: d.toDateString(),
        duration: this.getTimeDiff(this.stime, this.etime)
        };

      this.show = true;

      if (this.value ==  this.items[1])
      {
        this.gameUrl = "https://cdn.mos.cms.futurecdn.net/rLh7Dh7EKo8F6zmDtXYp8W.jpg"
      }
      if (this.value == this.items[2])
      {
        this.gameUrl = "https://images.pushsquare.com/c072e92b6753d/final-fantasy-vii-remake-how-long-how-long-to-beat-hours-ps4.original.jpg"
      }
      if (this.value == this.items[3])
      {
        this.gameUrl = "https://cdn.cloudflare.steamstatic.com/steam/apps/1555760/ss_39f101ac5077f49cac552b5b91b788793f1efde1.1920x1080.jpg?t=1614207961"
      }
      if(this.value == this.items[0])
      {
        this.gameUrl = "https://images.unsplash.com/photo-1619725002198-6a689b72f41d?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=2670&q=80"
      }
    }
  },
  data: () => ({
    items: [
      "Just Chatting",
      "Cyberpunk 2077",
      "Final Fantasy VII",
      "Black Desert",
    ],
    value: "Just Chatting",
    date: new Date(Date.now() - new Date().getTimezoneOffset() * 60000)
      .toISOString()
      .substr(0, 10),
    menu2: false,
    stime: "01:00",
    etime: "13:00",
    schedule: {},
    show: false,
    gameUrl: "https://images.unsplash.com/photo-1619725002198-6a689b72f41d?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=2670&q=80"
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
