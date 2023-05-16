<template>
  <v-card color="basil">
    <v-card-title class="text-center justify-center py-6">
      <h1 class="font-weight-bold text-h4 text-basil">
        POMODORO
      </h1>
    </v-card-title>

    <v-tabs
      v-model="tab"
      bg-color="transparent"
      color="basil"
      grow
    >
      <v-tab
        v-for="tab in tabTitles"
        :key="tab"
        :value="tab"
      >
        {{ tab }}
      </v-tab>
    </v-tabs>

    <v-window v-model="tab">
      <v-window-item
        v-for="tab in tabTitles"
        :key="tab"
        :value="tab"
      >
        <v-card
          color="basil"
          class="text-center pa-10"
          flat
        >
          <div class="text-h1 font-weight-bold">
            {{ displayMinutes }}:{{ displaySeconds }}
          </div>
        </v-card>
        <v-container class="text-center">
          <v-row justify="center">
            <v-col cols="4" sm="4" md="4">
              <v-btn @click="start()" 
              rounded="sm" 
              size="x-large" 
              class="bg-deep-purple">
                Start
              </v-btn>
            </v-col>
            <v-col cols="4" sm="4" md="4">
              <v-btn @click="stop()" 
              rounded="sm" 
              size="x-large" 
              class="bg-amber">
                Stop
              </v-btn>
            </v-col>
            <v-col cols="4" sm="4" md="4">
              <v-btn  @click="reset(tab)"
              rounded="sm" 
              size="x-large" 
              class="bg-black">
                Reset
              </v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-window-item>
    </v-window>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      tab: 'Pomodoro',
      tabTitles: ['Pomodoro', 'Short Break', 'Long Break'],
      timerInstance: null,
      totalSecond: 25 * 60,
    }
  },
  computed: {
    displayMinutes() {
      let minutes= Math.floor(this.totalSecond / 60);
      return this.formatTime(minutes)
    },
    displaySeconds() {
      let seconds= this.totalSecond % 60;
      return this.formatTime(seconds)
    },
  },
  watch: {
    tab(newVal) {
      this.reset(newVal);
    }
  },
  methods: {
    formatTime(time) {
      if (time < 10) {
        return '0'+ time
      }
      return time.toString()
    },
    start() {
      this.stop();
      this.timerInstance = setInterval(() => {
        this.totalSecond -=1
      }, 1000)
    },
    stop() {
      clearInterval(this.timerInstance)
    },
    reset(tab) {
      console.log('change tab');
      if (tab === 'Pomodoro') {
        this.totalSecond= 25 * 60
      }else if (tab === 'Short Break') {
        this.totalSecond= 5 * 60
      }else {
        this.totalSecond= 15 * 60
      }
    },
  },
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
