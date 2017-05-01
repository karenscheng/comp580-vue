<template>
  <div class="freeplay">

    <div class="container">

      <div id="heading" class="text" v-on:mouseover="instructionsMouseOver()">
        <p>Press keys on your keyboard to produce sounds!</p>
      </div>

    <div id="keys">

      <div class="keys">
        <div class="top-row">
          <div data-key="81" class="key" id="key-1">
            <span class="sound"></span>
          </div>
          <div data-key="87" class="key" id="key-2">
            <span class="sound"></span>
          </div>
          <div data-key="69" class="key" id="key-3">
            <span class="sound"></span>
          </div>
          <div data-key="82" class="key" id="key-4">
            <span class="sound"></span>
          </div>
          <div data-key="84" class="key" id="key-5">
            <span class="sound"></span>
          </div>
          <div data-key="89" class="key" id="key-6">
            <span class="sound"></span>
          </div>
          <div data-key="85" class="key" id="key-7">
            <span class="sound"></span>
          </div>
          <div data-key="73" class="key" id="key-8">
            <span class="sound"></span>
          </div>
          <div data-key="79" class="key" id="key-9">
            <span class="sound"></span>
          </div>
          <div data-key="80" class="key" id="key-10">
            <span class="sound"></span>
          </div>
        </div>
        <div class="middle-row">
          <div data-key="65" class="key" id="key-11">
            <span class="sound"></span>
          </div>
          <div data-key="83" class="key" id="key-12">
            <span class="sound"></span>
          </div>
          <div data-key="68" class="key" id="key-13">
            <span class="sound"></span>
          </div>
          <div data-key="70" class="key" id="key-14">
            <span class="sound"></span>
          </div>
          <div data-key="71" class="key" id="key-15">
            <span class="sound"></span>
          </div>
          <div data-key="72" class="key" id="key-16">
            <span class="sound"></span>
          </div>
          <div data-key="74" class="key" id="key-17">
            <span class="sound"></span>
          </div>
          <div data-key="75" class="key" id="key-18">
            <span class="sound"></span>
          </div>
          <div data-key="76" class="key" id="key-19">
            <span class="sound"></span>
          </div>
        </div>
        <div class="bottom-row">
          <div data-key="65" class="key" id="key-20">
            <span class="sound"></span>
          </div>
          <div data-key="83" class="key" id="key-21">
            <span class="sound"></span>
          </div>
          <div data-key="68" class="key" id="key-22">
            <span class="sound"></span>
          </div>
          <div data-key="70" class="key" id="key-23">
            <span class="sound"></span>
          </div>
          <div data-key="71" class="key" id="key-24">
            <span class="sound"></span>
          </div>
          <div data-key="72" class="key" id="key-25">
            <span class="sound"></span>
          </div>
          <div data-key="74" class="key" id="key-26">
            <span class="sound"></span>
          </div>
        </div>
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

      <div id = "return" @click="returnHome" v-on:mouseover="returnMouseOver()">
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
    instructionsMouseOver () {
      window.responsiveVoice.speak('Press keys on your keyboard to produce sounds!')
    },
    returnMouseOver () {
      window.responsiveVoice.speak('Back to homepage')
    },
    keyPressed (e) {
      // uncomment below for some transitions that dont work :)
      // var myDiv = document.querySelector('div[data-key="' + e.keyCode + '"]')
      // if (myDiv) {
      //   myDiv.classList.add('playing')
      //   myDiv.addEventListener('transitionend', this.removeClass())
      //   console.log(myDiv)
      // }
      // console.log('Just pressed key: ' + e.keyCode)
      //
      // this.soundMap.get(e.keyCode).play()

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
  background: linear-gradient(141deg, #0fb8ad 0%, #1fc8db 51%, #2cb5e8 75%);
}

.keys {
  align-items: center;
  justify-content: center;
}

.key {
  display: inline-block;
  border: 4px solid #2c3e50;
  border-radius: 5px;
  margin: 1rem;
  font-size: 1.5rem;
  padding: 1rem .5rem;
  transition:all .07s;
  width: 50px;
  height: 50px;
  text-align: center;
  color: white;
  background: rgba(256, 256, 256, 0.8);
}

#key-1{
  background-image: url('/static/icons/airplane.svg');
}

#key-2{
  background-image: url('/static/icons/tropical.svg');
}

#key-3{
  background-image: url('/static/icons/bad-weather.svg');
}

#key-4{
  background-image: url('/static/icons/canoe.svg');
}

#key-5{
  background-image: url('/static/icons/bed.svg');
}

#key-6{
  background-image: url('/static/icons/bell.svg');
}

#key-7{
  background-image: url('/static/icons/bench.svg');
}

#key-8{
  background-image: url('/static/icons/bus.svg');
}

#key-9{
  background-image: url('/static/icons/tent.svg');
}

#key-10{
  background-image: url('/static/icons/caravan.svg');
}

#key-11{
  background-image: url('/static/icons/carrier.svg');
}

#key-12{
  background-image: url('/static/icons/pamela.svg');
}

#key-13{
  background-image: url('/static/icons/diving.svg');
}

#key-14{
  background-image: url('/static/icons/hand-bag.svg');
}

#key-15{
  background-image: url('/static/icons/hat.svg');
}

#key-16{
  background-image: url('/static/icons/hot-air-balloon.svg');
}

#key-17{
  background-image: url('/static/icons/ice-cream.svg');
}

#key-18{
  background-image: url('/static/icons/map.svg');
}

#key-19{
  background-image: url('/static/icons/mountain.svg');
}

#key-20{
  background-image: url('/static/icons/postal.svg');
}

#key-21{
  background-image: url('/static/icons/sailboat.svg');
}

#key-22{
  background-image: url('/static/icons/sand-castle.svg');
}

#key-23{
  background-image: url('/static/icons/sandals.svg');
}

#key-24{
  background-image: url('/static/icons/ski.svg');
}

#key-25{
  background-image: url('/static/icons/surf.svg');
}

#key-26{
  background-image: url('/static/icons/sun-umbrella.svg');
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
  border: 5px solid #2c3e50;
}

#return:hover {
  background-color: #97d5b6;
}

</style>
