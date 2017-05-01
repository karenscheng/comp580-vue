<template>
<div id = "home">
  <h1>Welcome to Build-A-Beat! </h1>
  <h2>Please choose from our two modes: Record Mode and Freeplay Mode. Record Mode allows you to make a beat and play it back, where Freeplay Mode allows you to play for as long as you'd like.</h2>
  <div class="button-div">
    <div class="button" id="record" @click="startRecording">
      <p class="text">RECORD</p>
    </div>
    <div class = "button" id ="freeplay" @click="startPlaying">
      <p class="text">FREEPLAY</p>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'Home',
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

#home {
  padding: 10px;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

h1 {
  font-size: 50px;
  padding: 0;
  margin: 0;
  text-align: center;
}

h2 {
  font-size: 28px;
  font-weight: 200;
  text-align: center;
}

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
  cursor: pointer;
  border: 5px solid #2c3e50;
}

#record{
  background-color: #e67c84;
  height: 300px;
  margin-bottom: 10px;
}

#record:hover {
  background-color: #eb969c;
}

#freeplay{
  background-color: #6bc497;
  height: 150px;
}

#freeplay:hover {
  background-color: #97d5b6;
}

</style>
