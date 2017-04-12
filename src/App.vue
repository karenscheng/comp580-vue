<template>
  <div id="app">
    <Home v-if="home "@startRecording="startRecording" @startPlaying="startPlaying"></Home>
    <Record v-if="recording" :speed="this.speed" @done="finish" :soundMap="this.soundMap"></Record>
    <SetTempo v-if="tempo" @slowChosen="setTempo('slow')" @mediumChosen="setTempo('medium')" @fastChosen="setTempo('fast')"></SetTempo>
    <!-- <RecordPrompt v-show="recordprompt"></RecordPrompt> -->
    <Freeplay v-if="freeplay" @returnHome="returnHome" :soundMap="this.soundMap"></Freeplay>
  </div>
</template>

<script>
import Home from './components/Home'
import SetTempo from './components/SetTempo'
import RecordPrompt from './components/RecordPrompt'
import Freeplay from './components/Freeplay'
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
      freeplay: false,
      end: false,
      speed: 0,
      soundMap: null
    }
  },

  mounted () {
    console.log('App -> mounted.')
    this.setSoundMap()
  },

  components: {
    Home,
    SetTempo,
    RecordPrompt,
    Freeplay,
    Record,
    End
  },

  methods: {
    setSoundMap () {
      this.soundMap = new Map()

      soundMap.set(81, 'bubbles')
      soundMap.set(87, 'clay')
      soundMap.set(69, 'confetti')
      soundMap.set(82, 'corona')
      soundMap.set(84, 'dotted-spiral')
      soundMap.set(89, 'flash-1')
      soundMap.set(85, 'flash-2')
      soundMap.set(73, 'flash-3')
      soundMap.set(79, 'glimmer')
      soundMap.set(80, 'moon')
      soundMap.set(65, 'splits')
      soundMap.set(83, 'squiggle')
      soundMap.set(68, 'strike')
      soundMap.set(70, 'suspension')
      soundMap.set(71, 'timer')
      soundMap.set(72, 'ufo')
      soundMap.set(74, 'veil')
      soundMap.set(75, 'wipe')
      soundMap.set(76, 'tink')
      soundMap.set(90, 'pinwheel')
      soundMap.set(88, 'piston-1')
      soundMap.set(67, 'piston-2')
      soundMap.set(86, 'piston-3')
      soundMap.set(66, 'prism-1')
      soundMap.set(78, 'prism-2')
      soundMap.set(77, 'prism-3')

      // for(var key of soundMap.keys()) {
      //   var name = soundMap.get(key)
      //   var path = '/static/sounds/' + name + '.mp3'
      //   var sound = new Howl({
      //     src: [path]
      //   });
      //   soundMap.set(key, sound)
      // }
    },
    returnHome () {
      this.home = true
      this.freeplay = false
    },
    startRecording () {
      this.home = false
      this.tempo = true
    },
    startPlaying () {
      this.home = false
      this.freeplay = true
    },
    setTempo (speed) {
      console.log('in app, here is speed: ' + speed)

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
    },
    finish () {
      this.recording = false
      this.home = true
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
