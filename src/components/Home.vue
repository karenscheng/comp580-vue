<template>
<div id = "home">
  <div class="button" id="record" @click="startRecording">
    <p class="text">RECORD</p>
  </div>
  <div class = "button" id ="freeplay" @click="startPlaying">
    <p class="text">FREEPLAY</p>
  </div>
</div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'COMP580 Project',
      recordedSounds: [],
      firstKeyPressed: true,
      playBackDone: false,
      loop: false,
      play: false,
      record: false
    }
  },
  methods: {
    startRecording () {
      this.$emit('startRecording')
    },
    startPlaying () {
      this.$emit('startPlaying')
    }
  }
}
</script>

<style scoped>
.text{
  display: inline-block;
  margin: auto;
  font-family: sans-serif;
  font-size: 50px;
  pointer-events: none;
}

.button{
  position: relative;
  display: flex;
  align-items: center;
  width: 97vw;
  border-radius: 20px;
  margin: auto;
  text-align: center;
}

#record{
  background-color: #e67c84;
  height: 400px;
  margin-bottom: 10px;
}

#freeplay{
  background-color: #6bc497;
  height: 200px;
}
</style>
