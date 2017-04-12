<template>
  <div class="freeplay">

    <div class="container">

      <div id="heading" class="text">
        <p>Press keys to produce sounds!</p>
      </div>

    <div id="keys">

      <div class="keys">
        <div class="top-row">
          <div data-key="81" class="key">
            <span class="sound"></span>
          </div>
          <div data-key="87" class="key">
            <span class="sound"></span>
          </div>
          <div data-key="69" class="key">
            <span class="sound"></span>
          </div>
          <div data-key="82" class="key">
            <span class="sound"></span>
          </div>
          <div data-key="84" class="key">
            <span class="sound"></span>
          </div>
          <div data-key="89" class="key">
            <span class="sound"></span>
          </div>
          <div data-key="85" class="key">
            <span class="sound"></span>
          </div>
          <div data-key="73" class="key">
            <span class="sound"></span>
          </div>
          <div data-key="79" class="key">
            <span class="sound"></span>
          </div>
          <div data-key="80" class="key">
            <span class="sound"></span>
          </div>
        </div>
        <div class="middle-row">
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
        <div class="bottom-row">
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
        </div>
      </div>

      <!-- <audio data-key="81" src="static/sounds/bubbles.mp3"></audio>
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
      <audio data-key="77" src="static/sounds/prism-3.mp3"></audio> -->
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

  props: [
    'soundMap'
  ],

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

      this.soundMap.get(e.keyCode).play()

      // var audio = document.querySelector('audio[data-key="' + e.keyCode + '"]')
      // try {
      //   audio.currentTime = 0
      //   audio.play()
      // } catch (err) {
      //   console.log('Key pressed but no audio associated')
      // }
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
