<template>
  <div class="freeplay">

    <div class="container">

    <div id="keys">

      <div class="keys">
        <div data-key="65" class="key">
          <span class="sound"></span>
        </div>
        <div data-key="83" class="key">
          <span class="sound"></span>
        </div>
        <div data-key="68" class="key">
          <span class="sound"></span>
        </div>
        <div data-key="70" class="key">
          <span class="sound"></span>
        </div>
        <div data-key="71" class="key">
          <span class="sound"></span>
        </div>
        <div data-key="72" class="key">
          <span class="sound"></span>
        </div>
        <div data-key="74" class="key">
          <span class="sound"></span>
        </div>
        <div data-key="75" class="key">
          <span class="sound"></span>
        </div>
        <div data-key="76" class="key">
          <span class="sound"></span>
        </div>
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

      <div id = "return" @click="returnHome">
        <p class="text">go back to homepage</p>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'freeplay',

  created () {
    window.addEventListener('keydown', this.keyPressed)
  },

  methods: {
    keyPressed (e) {
      // uncomment below for some transitions that dont work :)
      // var myDiv = document.querySelector('div[data-key="' + e.keyCode + '"]')
      // if (myDiv) {
      //   myDiv.classList.add('playing')
      //   myDiv.addEventListener('transitionend', this.removeClass())
      //   console.log(myDiv)
      // }
      console.log('Just pressed key: ' + e.keyCode)

      var audio = document.querySelector('audio[data-key="' + e.keyCode + '"]')
      try {
        audio.currentTime = 0
        audio.play()
      } catch (err) {
        console.log('Key pressed but no audio associated')
      }
    },
    returnHome () {
      this.$emit('returnHome')
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

.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100vh;
}

.keys {
  /*display: flex;*/
  /*flex: 1;*/
  /*min-height: 100vh;*/
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
  color: white;
  background: white;
}

.playing-transition {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 10px #ffc600;
}

kbd {
  display: block;
  font-size: 40px;
}

.sound {
  font-size: 1.2rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: #ffc600;
}

#return{
  position: relative;
  display: flex;
  align-items: center;
  width: 97vw;
  border-radius: 20px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  background-color: #6bc497;
  height: 200px;
}

</style>
