<template>
  <v-card>
    <v-card-title>
      <span class="headline">Timer Options</span>
    </v-card-title>
    <v-card-text>
      <v-container>
        <v-row>
          <v-col cols="12" sm="6" md="4">
            <v-select
              v-model="focusDurationInMinutes"
              :items="[5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60]"
              label="Focus interval duration (in minutes)"
              required
            ></v-select>
          </v-col>
          <v-col cols="12" sm="6" md="4">
            <v-select
              v-model="pomosPerCycle"
              :items="[
                '2 intervals',
                '3 intervals',
                '4 intervals',
                '5 intervals',
                '6 intervals',
                '7 intervals',
                '8 intervals',
                '9 intervals',
                '10 intervals',
              ]"
              label="Long break after"
              required
            ></v-select>
          </v-col>
          <v-col cols="12" sm="6" md="4">
            <v-select
              v-model="shortBreakInMinutes"
              :items="Array.from(Array(11).keys())"
              label="Short break duration (in minutes)"
              required
            ></v-select>
          </v-col>
          <v-col cols="12" sm="6" md="4">
            <v-select
              v-model="longBreakInMinutes"
              :items="[0, 5, 10, 15, 20, 25, 30]"
              label="Long break duration (in minutes)"
              required
            ></v-select>
          </v-col>
        </v-row>
      </v-container>
    </v-card-text>
    <v-card-actions>
      <v-spacer></v-spacer>
      <v-btn color="blue darken-1" text @click="cancel">Cancel</v-btn>
      <v-btn color="blue darken-1" text @click="save">Save</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "PomoSettingsModal",
  data() {
    return {
      pomosPerCycle: "4 intervals",
    };
  },
  computed: {
    focusDurationInMinutes: {
      get() { return this.$store.state.pomoSettings.focusDurationInMinutes; },
      set(val) { this.$store.commit('SET_FOCUS_DURATION_IN_MINUTES', val) }
    },
    shortBreakInMinutes: {
      get() { return this.$store.state.pomoSettings.shortBreakInMinutes; },
      set(val) { this.$store.commit('SET_SHORT_BREAK_IN_MINUTES', val) }
    },
    longBreakInMinutes: {
      get() { return this.$store.state.pomoSettings.longBreakInMinutes; },
      set(val) { this.$store.commit('SET_LONG_BREAK_IN_MINUTES', val) }
    }
  },
  methods: {
    save() {
      let pomos = Number(this.pomosPerCycle.slice(0, 1));
      this.$store.commit('SET_POMOS_PER_CYCLE', pomos);
      this.$emit("on-save");
    },
    cancel() {
      this.$emit("on-cancel");
    },
  },
};
</script>

<style lang="scss" scoped></style>
