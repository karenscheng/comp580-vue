<template>
  <div class="play">
    <h1>{{ msg }}</h1>
    <h2>Step 1: Select a tempo</h2>
    <h2>Step 2: Hit 'record'</h2>
    <h2>Step 3: Hit keys!</h2>

    <div id = "selectAndRecord" class = "keys">
      <span id="selectbox" class = "key">
        <select id="select" class ="recordButton" >
            <option value='default'>SELECT TEMPO</option>
            <option value='80'>SLOW</option>
            <option value='120'>MEDIUM</option>
            <option value='140'>FAST</option>
          </select>
      </span>
      <div class = "key">
        <button id="record" class = "recordButton" @click="startRecording">RECORD</button>
      </div>
    </div>

    <div class="keys">
      <div data-key="65" class="key">
        <kbd>A</kbd>
        <span class="sound">clap</span>
      </div>
      <div data-key="83" class="key">
        <kbd>S</kbd>
        <span class="sound">hihat</span>
      </div>
      <div data-key="68" class="key">
        <kbd>D</kbd>
        <span class="sound">kick</span>
      </div>
      <div data-key="70" class="key">
        <kbd>F</kbd>
        <span class="sound">openhat</span>
      </div>
      <div data-key="71" class="key">
        <kbd>G</kbd>
        <span class="sound">boom</span>
      </div>
      <div data-key="72" class="key">
        <kbd>H</kbd>
        <span class="sound">ride</span>
      </div>
      <div data-key="74" class="key">
        <kbd>J</kbd>
        <span class="sound">snare</span>
      </div>
      <div data-key="75" class="key">
        <kbd>K</kbd>
        <span class="sound">tom</span>
      </div>
      <div data-key="76" class="key">
        <kbd>L</kbd>
        <span class="sound">tink</span>
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

  mounted () {
    console.log('Hello -> mounted')
    window.addEventListener('keydown', this.keyPressed)
  },

  beforeDestroy () {
    console.log('Hello -> beforeDestroy')
  },

  methods: {
    keyPressed (e) {
      console.log('Hello -> keyPressed')

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

      if (this.record) {
        console.log('start timer!')
        var tempo = document.getElementById('select').value
        var recordTime = this.getRecordTime()
        var vm = this

        if (this.firstKeyPressed) {
          setTimeout(function () {
            this.record = false
            // call to function that takes in an array and a tempo in order to set the time stamps correctly and set firstKeyPressed to true
            vm.quantize(tempo)
            this.firstKeyPressed = true
            console.log('end timer!')
          }, recordTime) // value from selector
          this.firstKeyPressed = false
        }

        var newDate = new Date().getTime()
        var newSound = {date: newDate, key: e.keyCode}

        this.recordedSounds.push(newSound)
        console.table(this.recordedSounds)
      }
    },
    removeClass (e) {
      console.log(e)
    },
    startRecording (e) {
      var tempo = document.getElementById('select').value
      if (tempo === 'default') {
        // document.getElementById('pressRecord').css('visibility', 'hidden')
        this.record = false
        console.log('can\'t record now')
      } else {
        console.log('recording!')
        this.record = true
      }
    },
    quantize (tempo) {
      var subdivision = 60 / tempo
      subdivision = subdivision / 4 // subdivision is how much time between each 16th note
      subdivision = subdivision * 1000 // convert subdivision to milliseconds

      console.log('tempo is ' + tempo)
      console.log('subdivision is: ' + subdivision)

      var initialTime = this.recordedSounds[0].date // sets the time of the first hit to adjust time of other hits to be relative
      var toSubtract = 0

      var i
      for (i = 0; i < this.recordedSounds.length; i++) {
        console.log('initial time: ' + this.recordedSounds[i].date)
        if (i === 0) {
          this.recordedSounds[i].date -= initialTime
          toSubtract += this.recordedSounds[i].date
        } else {
          this.recordedSounds[i].date -= initialTime
          this.recordedSounds[i].date -= toSubtract
          toSubtract += this.recordedSounds[i].date
        }
        console.log('new initial time: ' + this.recordedSounds[i].date)
      }

      var j
      for (j = 0; j < this.recordedSounds.length; j++) {
        var numSubdivisions = this.recordedSounds[j].date / subdivision // how many subdivisions fit in the raw time
        numSubdivisions = Math.round(numSubdivisions) // round to the nearest 16th note
        console.log('number of subdivisions: ' + numSubdivisions)
        this.recordedSounds[j].date = numSubdivisions * subdivision // adjust new time to the time of a 16th note
        console.log('this key plays this many milliseconds after playback starts: ' + this.recordedSounds[j].date)
      }

      this.loopIt()
    },
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
    getRecordTime () {
      var tempo = document.getElementById('select').value
      tempo = (60 / tempo) * 8000
      return tempo
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.keys {
  display: flex;
  flex: 1;
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
  width: 100px;
  text-align: center;
  color: white;
  background: rgba(0,0,0,0.4);
  text-shadow: 0 0 5px black;
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

.recordButton{
  border: none;
  outline: none;
  background: none;
  text-decoration: none;
  color: white;
  font-size: 1.5rem;
  text-shadow: 0 0 5px black;
}

#selectbox{
  width: 150px;
}

</style>
