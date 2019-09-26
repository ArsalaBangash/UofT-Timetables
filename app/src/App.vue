<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>UofT Timetable Planner</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        href="https://github.com/ArsalaBangash/UofT-Timetables"
        target="_blank"
        fab
        rounded
        class="ma-2"
        color="primary"
      >
        <v-icon>fab fa-github</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <Planner/>
    </v-content>
  </v-app>
</template>

<script>
import Planner from "./components/Planner";

export default {
  name: "App",
  components: {
    Planner
  },
  data: () => ({
    //
  })
};
</script>

