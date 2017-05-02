<template>
  <div class = "recordprompt">
    <div v-if="first">
      <h1>You can practice playing with the tempo, when you are ready to record, press
      the button at the bottom of the screen. Press any button to continue</h1>
    </div>
    <div v-if="!first">
      <h1>We will start recording once you start playing! Press Enter to continue.</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: 'recordprompt',

  props: [
    'first'
  ],

  created () {
    window.addEventListener('keydown', this.keyPressed)
    if (this.first) {
      window.responsiveVoice.speak('You can practice playing with the tempo, when you are ready to record, press' +
      'the button at the bottom of the screen. Press any button to continue')
    } else {
      window.responsiveVoice.speak('We will start recording once you start playing! Press Enter to continue.')
    }
  },

  methods: {
    keyPressed (e) {
      window.responsiveVoice.cancel()
      if (this.first) {
        this.$emit('startTempo')
      } else {
        if (e.keyCode === 13) {
          this.$emit('startRecording')
        }
      }
    }
  }
}

</script>

<style scoped>

.recordprompt {
  background: linear-gradient(141deg, #0fb8ad 0%, #1fc8db 51%, #2cb5e8 75%);
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

h1{
  font-size: 32px;
}

</style>
