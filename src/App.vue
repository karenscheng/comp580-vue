<template>
  <div id="app">
    <Home v-show="home "@startRecording="startRecording" @startPlaying="startPlaying"></Home>
    <Record v-show="recording" :tempo="this.speed"></Record>
    <SetTempo v-show="tempo" @slowChosen="setTempo('slow')" @mediumChosen="setTempo('medium')" @fastChosen="setTempo('fast')"></SetTempo>
    <!-- <RecordPrompt v-show="recordprompt"></RecordPrompt> -->
    <End v-show="end"></End>
  </div>
</template>

<script>
import Home from './components/Home'
import SetTempo from './components/SetTempo'
import RecordPrompt from './components/RecordPrompt'
import Record from './components/Record'
import End from './components/End'

export default {
  name: 'app',

  data () {
    return {
      home: true,
      recording: false,
      tempo: false,
      recordprompt: false,
      end: false,
      speed: 0
    }
  },

  mounted () {
    console.log('App -> mounted.')
  },

  components: {
    Home,
    SetTempo,
    RecordPrompt,
    Record,
    End
  },

  methods: {
    startRecording () {
      this.home = false
      this.tempo = true
    },
    startPlaying () {
      this.home = false
      this.play = true
    },
    setTempo (speed) {
      console.log(speed)

      if (speed === 'slow') {
        this.speed = 80
      }
      if (speed === 'medium') {
        this.speed = 120
      }
      if (speed === 'fast') {
        this.speed = 140
      }

      this.recording = true
      this.tempo = false
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
  margin-bottom: 10px;
}

html {
  font-size: 10px;
  /*background: url(http://i.imgur.com/b9r5sEL.jpg) bottom center;*/
  background-size: cover;
}

body,html {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}

</style>
