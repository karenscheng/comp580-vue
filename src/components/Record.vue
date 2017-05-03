<template>
  <div class="record">
    <RecordPrompt v-if="prompt" :first="first" @startTempo="startTempo" @startRecording="startRecording"></RecordPrompt>
    <End v-if="end" :recordedSounds="recordedSounds" :speed="speed" @done="finish" @addlayer="addLayer"></End>

    <div id="keys" v-if="recording">

      <div class="keys">
        <div class="top-row">
          <div data-key="81" class="key" id="key-1">
            <span class="sound"></span>
          </div>
          <div data-key="87" class="key" id="key-2">
            <span class="sound"></span>
          </div>
          <div data-key="69" class="key" id="key-3">
            <span class="sound"></span>
          </div>
          <div data-key="82" class="key" id="key-4">
            <span class="sound"></span>
          </div>
          <div data-key="84" class="key" id="key-5">
            <span class="sound"></span>
          </div>
          <div data-key="89" class="key" id="key-6">
            <span class="sound"></span>
          </div>
          <div data-key="85" class="key" id="key-7">
            <span class="sound"></span>
          </div>
          <div data-key="73" class="key" id="key-8">
            <span class="sound"></span>
          </div>
          <div data-key="79" class="key" id="key-9">
            <span class="sound"></span>
          </div>
          <div data-key="80" class="key" id="key-10">
            <span class="sound"></span>
          </div>
        </div>
        <div class="middle-row">
          <div data-key="65" class="key" id="key-11">
            <span class="sound"></span>
          </div>
          <div data-key="83" class="key" id="key-12">
            <span class="sound"></span>
          </div>
          <div data-key="68" class="key" id="key-13">
            <span class="sound"></span>
          </div>
          <div data-key="70" class="key" id="key-14">
            <span class="sound"></span>
          </div>
          <div data-key="71" class="key" id="key-15">
            <span class="sound"></span>
          </div>
          <div data-key="72" class="key" id="key-16">
            <span class="sound"></span>
          </div>
          <div data-key="74" class="key" id="key-17">
            <span class="sound"></span>
          </div>
          <div data-key="75" class="key" id="key-18">
            <span class="sound"></span>
          </div>
          <div data-key="76" class="key" id="key-19">
            <span class="sound"></span>
          </div>
        </div>
        <div class="bottom-row">
          <div data-key="65" class="key" id="key-20">
            <span class="sound"></span>
          </div>
          <div data-key="83" class="key" id="key-21">
            <span class="sound"></span>
          </div>
          <div data-key="68" class="key" id="key-22">
            <span class="sound"></span>
          </div>
          <div data-key="70" class="key" id="key-23">
            <span class="sound"></span>
          </div>
          <div data-key="71" class="key" id="key-24">
            <span class="sound"></span>
          </div>
          <div data-key="72" class="key" id="key-25">
            <span class="sound"></span>
          </div>
          <div data-key="74" class="key" id="key-26">
            <span class="sound"></span>
          </div>
        </div>
      </div>

      <div v-if="ready" class="cancel button" @click="goHome" v-on:mouseover="cancelMouseOver()">
        <p class="text">cancel</p>
      </div>

      <div v-if="!ready" class="start button" @click="readyPrompt" v-on:mouseover="startMouseOver()">
        <p class="text">start recording</p>
      </div>

      <audio data-key="81" src="static/sounds/bubbles.mp3"></audio>
      <audio data-key="87" src="static/sounds/clay.mp3"></audio>
      <audio data-key="69" src="static/sounds/confetti.mp3"></audio>
      <audio data-key="82" src="static/sounds/corona.mp3"></audio>
      <audio data-key="84" src="static/sounds/dotted-spiral.mp3"></audio>
      <audio data-key="89" src="static/sounds/flash-1.mp3"></audio>
      <audio data-key="85" src="static/sounds/flash-2.mp3"></audio>
      <audio data-key="73" src="static/sounds/flash-3.mp3"></audio>
      <audio data-key="79" src="static/sounds/glimmer.mp3"></audio>
      <audio data-key="80" src="static/sounds/moon.mp3"></audio>

      <audio data-key="65" src="static/sounds/splits.mp3"></audio>
      <audio data-key="83" src="static/sounds/squiggle.mp3"></audio>
      <audio data-key="68" src="static/sounds/strike.mp3"></audio>
      <audio data-key="70" src="static/sounds/suspension.mp3"></audio>
      <audio data-key="71" src="static/sounds/timer.mp3"></audio>
      <audio data-key="72" src="static/sounds/ufo.mp3"></audio>
      <audio data-key="74" src="static/sounds/veil.mp3"></audio>
      <audio data-key="75" src="static/sounds/wipe.mp3"></audio>
      <audio data-key="76" src="static/sounds/tink.wav"></audio>

      <audio data-key="90" src="static/sounds/pinwheel.mp3"></audio>
      <audio data-key="88" src="static/sounds/piston-1.mp3"></audio>
      <audio data-key="67" src="static/sounds/piston-2.mp3"></audio>
      <audio data-key="86" src="static/sounds/piston-3.mp3"></audio>
      <audio data-key="66" src="static/sounds/prism-1.mp3"></audio>
      <audio data-key="78" src="static/sounds/prism-2.mp3"></audio>
      <audio data-key="77" src="static/sounds/prism-3.mp3"></audio>
      </div>
    </div>
</template>

<script>
import RecordPrompt from './RecordPrompt'
import End from './End'

export default {
  name: 'record',

  props: [
    'speed'
  ],

  data () {
    return {
      msg: 'COMP580 Project',
      recordedSounds: [],
      layeredSounds: [],
      firstKeyPressed: true,
      playBackDone: false,
      play: false,
      record: true,
      prompt: true,
      ready: false,
      recording: false,
      end: false,
      loopTempo: null,
      loopRecording: null,
      layer: false,
      initialTime: 0,
      first: true
    }
  },

  created () {
    window.addEventListener('keydown', this.keyPressed)
  },

  components: {
    RecordPrompt,
    End
  },

  methods: {
    cancelMouseOver () {
      window.responsiveVoice.speak('Cancel')
    },
    startMouseOver () {
      window.responsiveVoice.speak('Start recording')
    },
    readyPrompt () {
      this.prompt = true
      this.recording = false
      this.first = false
    },
    startRecording () {
      // const tempo = this.speed
      // this.startTempo()
      this.ready = true
      this.prompt = false
      if (!this.end) {
        this.recording = true
      }
    },
    startTempo () {
      this.playTempo()
      this.prompt = false
      this.ready = false

      if (!this.end) {
        this.recording = true
      }
    },
    playTempo () {
      var tempo = 60 / this.speed * 1000
      var vm = this
      this.loopTempo = setInterval(function () {
        vm.playClick(76)
      }, tempo)
    },
    playClick (index) {
      var audioString = 'audio[data-key="' + index + '"]'
      var audio = document.querySelector(audioString)
      audio.currentTime = 0
      audio.play()
    },
    keyPressed (e) {
      if (this.ready) {
        this.record = true
      }

      if (!this.end) {
        var audio = document.querySelector('audio[data-key="' + e.keyCode + '"]')
        try {
          audio.currentTime = 0
          audio.play()
        } catch (err) {
          console.log('Key pressed but no audio associated')
          this.record = false
        }
      }

      if (this.record) {
        const tempo = this.speed
        var recordTime = this.getRecordTime()
        var vm = this

        if (this.firstKeyPressed) {
          setTimeout(function () {
            this.record = false
            this.end = true
            this.recording = false
            // call to function that takes in an array and a tempo in order to set the time stamps correctly and set firstKeyPressed to true
            vm.quantize(tempo)
            this.firstKeyPressed = true
          }, recordTime) // value from selector
          this.firstKeyPressed = false
        }

        var newDate = new Date().getTime()
        var newSound = {date: newDate, key: e.keyCode}

        if (this.layer) {
          this.layeredSounds.push(newSound)
        } else {
          this.recordedSounds.push(newSound)
        }
      }
    },
    removeClass (e) {
      console.log(e)
    },
    quantize (tempo) {
      var sounds
      var vm = this

      if (vm.layer) {
        sounds = vm.layeredSounds
      } else {
        sounds = vm.recordedSounds
      }

      var subdivision = 60 / tempo
      subdivision = subdivision / 2 // subdivision is how much time between each 16th note
      subdivision = subdivision * 1000 // convert subdivision to milliseconds

      if (!vm.layer) {
        vm.initialTime = sounds[0].date // sets the time of the first hit to adjust time of other hits to be relative
      }

      var i
      for (i = 0; i < sounds.length; i++) {
        if (sounds[i].date <= vm.initialTime) {
          if (vm.layer) {
            sounds[i].date += vm.getRecordTime()
          }
          // vm.initalTime -= this.getRecordTime()
        }
        sounds[i].date %= vm.initialTime
        if (vm.layer) {
          sounds[i].date %= vm.getRecordTime()
        }
      }

      var j
      for (j = 0; j < sounds.length; j++) {
        var numSubdivisions = sounds[j].date / subdivision // how many subdivisions fit in the raw time
        numSubdivisions = Math.round(numSubdivisions) // round to the nearest 16th note
        sounds[j].date = numSubdivisions * subdivision // adjust new time to the time of a 16th note
      }

      if (vm.layer) {
        vm.sortSounds()
        clearTimeout(vm.loopRecording)
      }

      // this.loopIt()
      vm.end = true
      clearInterval(vm.loopTempo)
      vm.record = false
      vm.recording = false
    },
    getRecordTime () {
      // var tempo = document.getElementById('select').value
      var tempo = this.speed
      tempo = (60 / tempo) * 8000
      return tempo
    },
    playRecording (index) {
      var playback
      var vm = this

      if (this.recordedSounds[index] === undefined) {
        clearTimeout(playback)
        this.playbackDone = true
      }

      this.playSound(this.recordedSounds, index - 1)

      if (!this.playbackDone) {
        playback = setTimeout(function () {
          vm.playRecording(index + 1)
        }, this.recordedSounds[index].date - this.recordedSounds[index - 1].date)
      } else {
        this.playbackDone = false
      }
    },
    playSound (sound, index) {
      var audioString = 'audio[data-key="' + sound[index].key + '"]'
      var audio = document.querySelector(audioString)
      audio.currentTime = 0
      audio.play()
    },
    loopIt () {
      var recordTime = this.getRecordTime()
      var vm = this

      vm.initialTime = new Date().getTime()
      vm.playRecording(1)
      this.loopRecording = setTimeout(function () {
        vm.playRecording(1)
        vm.loopIt(this.recordedSounds)
      }, recordTime)
    },
    addLayer () {
      this.end = false
      this.record = true
      this.recording = true
      this.layer = true
      this.firstKeyPressed = true
      this.playTempo()
      this.loopIt()
    },
    sortSounds () {
      var x
      var y

      for (x = 0; x < this.layeredSounds.length; x++) {
        this.recordedSounds.push(this.layeredSounds[x])
      }

      for (x = 0; x < this.recordedSounds.length; x++) {
        for (y = x; y < this.recordedSounds.length; y++) {
          if (this.recordedSounds[y].date < this.recordedSounds[x].date) {
            var temp = this.recordedSounds[x]
            this.recordedSounds[x] = this.recordedSounds[y]
            this.recordedSounds[y] = temp
          }
        }
      }

      for (x = 0; x < this.recordedSounds.length; x++) {
        console.log(this.recordedSounds[x])
      }
    },
    finish () {
      this.recordedSounds = []
      this.$emit('done')
      this.end = false
    },
    goHome () {
      window.location = '/'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.record {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  background: linear-gradient(141deg, #0fb8ad 0%, #1fc8db 51%, #2cb5e8 75%);
}

.keys {
  align-items: center;
  justify-content: center;
}

.key {
  display: inline-block;
  border: 4px solid black;
  border-radius: 5px;
  margin: 1rem;
  font-size: 1.5rem;
  padding: 1rem .5rem;
  transition:all .07s;
  width: 50px;
  height: 50px;
  text-align: center;
  background: rgba(256, 256, 256, 0.8);
  background-image: url('/static/icons/airplane.svg');
}

h1{
  font-size: 28px;
  text-align: center;
  margin-bottom: 8vh;
}

.sound {
  font-size: 1.2rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #ffc600;
}

.recordButton{
  border: none;
  outline: none;
  background: none;
  text-decoration: none;
  color: white;
  font-size: 1.5rem;
  text-shadow: 0 0 5px black;
}

#selectbox{
  width: 150px;
}

.button {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 60vw;
  height: 20vh;

  border-radius: 20px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  border: 5px solid #2c3e50;
}

.cancel {
  background-color: #e67c84;
  margin-top: 10vh;
}

.cancel:hover {
  background-color: #eb969c;
}

.cancel .text, .start .text {
  font-size: 34px;
}

.start {
  margin-top: 10vh;
  background-color: #6bc497;
}

.start:hover {
  background-color: #97d5b6;
}

#key-1{
  background-image: url('/static/icons/airplane.svg');
}

#key-2{
  background-image: url('/static/icons/tropical.svg');
}

#key-3{
  background-image: url('/static/icons/bad-weather.svg');
}

#key-4{
  background-image: url('/static/icons/canoe.svg');
}

#key-5{
  background-image: url('/static/icons/bed.svg');
}

#key-6{
  background-image: url('/static/icons/bell.svg');
}

#key-7{
  background-image: url('/static/icons/bench.svg');
}

#key-8{
  background-image: url('/static/icons/bus.svg');
}

#key-9{
  background-image: url('/static/icons/tent.svg');
}

#key-10{
  background-image: url('/static/icons/caravan.svg');
}

#key-11{
  background-image: url('/static/icons/carrier.svg');
}

#key-12{
  background-image: url('/static/icons/pamela.svg');
}

#key-13{
  background-image: url('/static/icons/diving.svg');
}

#key-14{
  background-image: url('/static/icons/hand-bag.svg');
}

#key-15{
  background-image: url('/static/icons/hat.svg');
}

#key-16{
  background-image: url('/static/icons/hot-air-balloon.svg');
}

#key-17{
  background-image: url('/static/icons/ice-cream.svg');
}

#key-18{
  background-image: url('/static/icons/map.svg');
}

#key-19{
  background-image: url('/static/icons/mountain.svg');
}

#key-20{
  background-image: url('/static/icons/postal.svg');
}

#key-21{
  background-image: url('/static/icons/sailboat.svg');
}

#key-22{
  background-image: url('/static/icons/sand-castle.svg');
}

#key-23{
  background-image: url('/static/icons/sandals.svg');
}

#key-24{
  background-image: url('/static/icons/ski.svg');
}

#key-25{
  background-image: url('/static/icons/surf.svg');
}

#key-26{
  background-image: url('/static/icons/sun-umbrella.svg');
}

</style>
