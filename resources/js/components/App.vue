<template>
  <v-app id="inspire">
    <v-app-bar app shrink-on-scroll>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>Turbine Inspector</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-row>
          <v-col v-for="turbine in turbines" :key="turbine.id" cols="2">
            <v-card :class="[isWorking ? workingClass : '', errorClass]" height="200">
              <v-card-title>Turbine number {{ turbine.id }}</v-card-title>
              <v-card-subtitle>{{ turbine.status }}</v-card-subtitle>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>


<script>
import Card from "./Card";
export default {
  components: {
    Card,
  },
  data: () => ({
    turbines: [],
    loaded: false
  }),
  beforeMount() {
    this.axios.get(`http://127.0.0.1/api/turbines`).then((response) => {
      this.turbines = response.data;
    });

    this.axios.get(`http://127.0.0.1/api/inspectTurbines`).then((response) => {
      console.log(response.data)
    });
  },
};
</script>
