<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row>
          <v-col sm="6" offset-sm="3">
            <pompdoro-app />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
</v-app>
  
</template>

<script>
import Pomodoro from './components/Pomodoro.vue'

export default {
  name: 'App',
  components: {
    'pompdoro-app': Pomodoro
  }
}
</script>

<style>
.v-application__wrap {
  max-height: 100%;
}
</style>
