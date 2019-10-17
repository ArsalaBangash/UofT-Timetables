<template>
  <v-stepper v-model="step
  ">
    <v-stepper-header>
      <v-stepper-step :complete="step
       > 1" step="1">Days off</v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step :complete="step
       > 2" step="2">Start and End Times</v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step step="3">Required/Optional Courses</v-stepper-step>
    </v-stepper-header>

    <v-stepper-items>
      <v-stepper-content step="1">
        <div height="200px">
          <div class="title">Which days would you like off?</div>
          <div class="d-flex justify-space-around">
            <v-checkbox v-for="day in days" :key="day" v-model="selectedDays" :label="day" :value="day"></v-checkbox>
          </div>
        </div>

        <v-btn color="primary" @click="step
           = 2">Continue</v-btn>
      </v-stepper-content>

      <v-stepper-content step="2">
        <v-card class="mb-12" color="grey lighten-1" height="300px">
          <v-calendar 
            type="week"
            :first-interval="intervals.first"
            :interval-minutes="intervals.minutes"
            :interval-count="intervals.count"
            :interval-height="intervals.height"
            :weekdays="schoolDays"
            :events="events"
            @click:time="timeClicked"
          ></v-calendar>
        </v-card>

        <v-btn color="primary" @click="step
           = 3">Continue</v-btn>

        <v-btn text @click="step = 1">Back</v-btn>
      </v-stepper-content>

      <v-stepper-content step="3">
        <v-card class="mb-12" color="grey lighten-1" height="200px"></v-card>

        <v-btn color="primary" @click="step
           = 1">Continue</v-btn>

        <v-btn text @click="step = 2">Back</v-btn>
      </v-stepper-content>
    </v-stepper-items>
  </v-stepper>
</template>

<script>
export default {
  computed: {
    schoolDays() {
      const selectedDayNumbers = this.selectedDays.map(day => this.dayMapping[day])
      return this.weekdays.filter(dayNumber => !selectedDayNumbers.includes(dayNumber))
    }
  },
  data() {
    return {
      step: 0,
      selectedDays: [],
      weekdays: [1, 2, 3, 4, 5],
      dayMapping: {
        Monday: 1,
        Tuesday: 2,
        Wednesday: 3,
        Thursday: 4,
        Friday: 5
      },
      days: ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
      intervals: { first: 6, minutes: 60, count: 16, height: 40 },
      events: []
    };
  },
  methods:{
    timeClicked(time){
      console.log(time)
      const event_start = time.date + " " + time.time.substring(0,2) + ":00"
      var event = {
        name: "Start of the day",
        start: event_start
      }
      this.events.push(event)
      console.log(event)
    }
  }
};
</script>