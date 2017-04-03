<template>
<div id = "end">
</div>
</template>

<script>

export default {
  name: 'end',

  props: [
    'recordedSounds'
  ],

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
    }
  }
}

</script>
