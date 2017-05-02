<template>
<div id = "SetTempo">
  <h1 v-on:mouseover="sayTempo">Select Tempo!</h1>

  <div id = "circle-div">
    <div id = "slow" class="circle" @click="slowTempo" v-on:mouseover="slowMouseOver()"><span class="circle-text">Slow</span></div>
    <div id = "medium" class="circle" @click="mediumTempo" v-on:mouseover="mediumMouseOver()"><span class="circle-text">Medium</span></div>
    <div id = "fast" class="circle" @click="fastTempo" v-on:mouseover="fastMouseOver()"><span class="circle-text">Fast</span></div>
  </div>
</div>
</template>

<script>
export default {
  name: 'settempo',

  // data () {
  //   return {
  //   }
  // },

  methods: {
    sayTempo () {
      window.responsiveVoice.speak('Select tempo')
    },
    slowMouseOver () {
      window.responsiveVoice.speak('Slow')
    },
    mediumMouseOver () {
      window.responsiveVoice.speak('Medium')
    },
    fastMouseOver () {
      window.responsiveVoice.speak('Fast')
    },
    slowTempo () {
      this.$emit('slowChosen')
    },
    mediumTempo () {
      this.$emit('mediumChosen')
    },
    fastTempo () {
      this.$emit('fastChosen')
    }
  }
}

</script>

<style scoped>

#SetTempo {
  padding-top: 10px;
  height: 100vh;
  width: 100vw;
}

h1 {
  font-size: 80px;
  font-family: sans-serif;
}

#circle-div {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.circle{
  border-radius: 50%;
  width: 30vw;
  height: 30vw;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.circle-text{
  font-size: 60px;
  font-family: sans-serif;
}

#slow{
  background-color: #e67c84;
}

#slow:hover {
  background-color: #eb969c;
}

#medium{
  background-color: #f5f299;
}

#medium:hover {
  background-color: #f7f4ad;
}

#fast{
  background-color: #6bc497;
}

#fast:hover {
  background-color: #97d5b6;
}
</style>
