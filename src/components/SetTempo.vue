<template>
<div id = "SetTempo">
  <h1>Select Tempo!</h1>

  <div id = "circle-div">
    <div id = "slow" class="circle" @click="slowTempo"><span class="circle-text">Slow</span></div>
    <div id = "medium" class="circle" @click="mediumTempo"><span class="circle-text">Medium</span></div>
    <div id = "fast" class="circle" @click="fastTempo"><span class="circle-text">Fast</span></div>
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

#medium{
  background-color: #f5f299;
}

#fast{
  background-color: #6bc497;
}
</style>
