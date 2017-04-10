<template>
<div id = "end">
  <div class="play-btn button" @click="togglePlay" v-if="play">
    <p class="text">play recording</p>
  </div>
  <div class="stop-btn button" @click="togglePlay" v-else>
    <p class="text">stop recording</p>
  </div>
  <div class="layer-btn button">
    <p class="text">layer beat</p>
  </div>
  <div class="start-over button" @click="startOver">
    <p class="text">START OVER</p>
  </div>
  <audio data-key="65" src="static/sounds/clap.wav"></audio>
  <audio data-key="83" src="static/sounds/hihat.wav"></audio>
  <audio data-key="68" src="static/sounds/kick.wav"></audio>
  <audio data-key="70" src="static/sounds/openhat.wav"></audio>
  <audio data-key="71" src="static/sounds/boom.wav"></audio>
  <audio data-key="72" src="static/sounds/ride.wav"></audio>
  <audio data-key="74" src="static/sounds/snare.wav"></audio>
  <audio data-key="75" src="static/sounds/tom.wav"></audio>
  <audio data-key="76" src="static/sounds/tink.wav"></audio>
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
      loop: null
    }
  },

  methods: {
    playRecording (index) {
      var playback
      var vm = this
      console.log('time to play the ' + index + 'sound in array')

      if (this.recordedSounds[index] === undefined) {
        console.log('stopping playback on index: ' + index)
        clearTimeout(playback)
        this.playbackDone = true
      }

      this.playSound(this.recordedSounds, index - 1)

      if (!this.playbackDone) {
        playback = setTimeout(function () {
          console.log('in timeout function')
          vm.playRecording(index + 1)
        }, this.recordedSounds[index].date)
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

      vm.playRecording(1)
      this.loop = setTimeout(function () {
        vm.playRecording(1)
        vm.loopIt(this.recordedSounds)
      }, recordTime)
    },
    togglePlay () {
      this.play = !this.play
      if (!this.play) {
        this.loopIt()
      } else {
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

.stop-btn {
  background-color: #e67c84;
  height: 30vh;
  margin-bottom: 2vh;
}

.layer-btn {
  background-color: #BDBEC0;
  height: 18vh;
  margin-bottom: 2vh;
}

.start-over {
  border: 3px solid black;
  height: 40vh;
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
