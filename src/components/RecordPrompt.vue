<template>
<div class = "recordprompt">
  <h1>We will start recording once you start playing! Press Enter to continue.</h1>
</div>
</template>

<script>
export default {
  name: 'recordprompt',
  mounted () {

  },
  created () {
    window.addEventListener('keydown', this.keyPressed)
    window.responsiveVoice.speak('Press keys on your keyboard to make sound, press enter to start!')
  },
  methods: {
    keyPressed (e) {
      this.$emit('start')
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
