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
  <div class="start-over button">
    <p class="text">START OVER</p>
  </div>
</div>
</template>

<script>

export default {
  name: 'end',

  props: [
    'recordedSounds'
  ],

  data () {
    return {
      play: true
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

      setTimeout(function () {
        vm.playRecording(1)
        vm.loopIt(this.recordedSounds)
      }, recordTime)
    },
    togglePlay () {
      this.play = !this.play
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
