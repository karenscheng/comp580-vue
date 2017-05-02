<template>
<div id = "end">
  <div class="play-btn button" @click="togglePlay" v-if="play" v-on:mouseover="playMouseOver()">
    <p class="text">play recording</p>
  </div>
  <div class="stop-btn button" @click="togglePlay" v-else v-on:mouseover="stopMouseOver()">
    <p class="text">stop recording</p>
  </div>
  <div v-if="!playing" class="layer-btn button" @click="addLayer" v-on:mouseover="addLayerMouseOver()">
    <p class="text">layer beat</p>
  </div>
  <div class="start-over button" @click="startOver" v-on:mouseover="startOverMouseOver()">
    <p class="text">START OVER</p>
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
</template>

<script>

export default {
  name: 'end',

  props: [
    'recordedSounds',
    'speed'
  ],

  data () {
    return {
      play: true,
      playing: false,
      loop: null,
      playback: null
    }
  },

  methods: {
    playMouseOver () {
      window.responsiveVoice.speak('Play Recording')
    },
    stopMouseOver () {
      window.responsiveVoice.speak('Stop')
    },
    addLayerMouseOver () {
      window.responsiveVoice.speak('Layer Beat')
    },
    startOverMouseOver () {
      window.responsiveVoice.speak('Start Over')
    },
    playRecording (index) {
      var vm = this
      console.log('time to play the ' + index + 'sound in array')

      if (this.recordedSounds[index] === undefined) {
        console.log('stopping playback on index: ' + index)
        clearTimeout(this.playback)
        this.playbackDone = true
      }

      this.playSound(this.recordedSounds, index - 1)

      if (!this.playbackDone) {
        this.playback = setTimeout(function () {
          console.log('in timeout function')
          vm.playRecording(index + 1)
        }, this.recordedSounds[index].date - this.recordedSounds[index - 1].date)
      } else {
        this.playbackDone = false
      }
    },
    playSound (sound, index) {
      var audioString = 'audio[data-key="' + sound[index].key + '"]'
      console.log(audioString)
      var audio = document.querySelector(audioString)
      audio.currentTime = 0
      audio.play()
    },
    loopIt () {
      var recordTime = this.getRecordTime()
      var vm = this

      vm.playRecording(1)
      this.loop = setTimeout(function () {
        vm.playRecording(1)
        vm.loopIt(this.recordedSounds)
      }, recordTime)
    },
    togglePlay () {
      this.play = !this.play
      if (!this.play) {
        this.playing = true
        this.loopIt()
      } else {
        this.playing = false
        clearTimeout(this.playback)
        clearTimeout(this.loop)
      }
    },
    getRecordTime () {
      // var tempo = document.getElementById('select').value
      var tempo = this.speed
      tempo = (60 / tempo) * 8000
      return tempo
    },
    startOver () {
      this.$emit('done')
    },
    addLayer () {
      this.$emit('addlayer')
    }
  }
}

</script>

<style scoped>

.button {
  position: relative;
  display: flex;
  align-items: center;
  width: 97vw;
  border-radius: 20px;
  margin: auto;
  text-align: center;
  cursor: pointer;
}

.play-btn {
  background-color: #6bc497;
  height: 30vh;
  margin-bottom: 2vh;
}

.play-btn:hover {
  background-color: #97d5b6;
}

.stop-btn {
  background-color: #e67c84;
  height: 30vh;
  margin-bottom: 2vh;
}

.stop-btn:hover {
  background-color: #eb969c;
}

.layer-btn {
  background-color: #D3D3D3;
  height: 18vh;
  margin-bottom: 2vh;
}

.start-over {
  border: 3px solid black;
  height: 40vh;
  background-color: rgba(256, 256, 256, 0.8);
}

.start-over .text {
  font-size: 70px;
}

.text{
  display: inline-block;
  margin: auto;
  font-family: sans-serif;
  font-size: 50px;
  pointer-events: none;
  -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
     -khtml-user-select: none; /* Konqueror HTML */
       -moz-user-select: none; /* Firefox */
        -ms-user-select: none; /* Internet Explorer/Edge */
            user-select: none; /* Non-prefixed version, currently
                                  supported by Chrome and Opera */
}

</style>
