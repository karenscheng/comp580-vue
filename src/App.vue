<template>
  <div id="app">
    <play></play>
  </div>
</template>

<script>
import Home from './components/Home'
import SetTempo from './components/SetTempo'
import RecordPrompt from './components/RecordPrompt'
import Play from './components/Play'
import End from './components/End'

export default {
  name: 'app',

  mounted () {
    console.log('App -> mounted.')
  },

  components: {
    Home,
    SetTempo,
    RecordPrompt,
    Play,
    End
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

html {
  font-size: 10px;
  /*background: url(http://i.imgur.com/b9r5sEL.jpg) bottom center;*/
  background-size: cover;
}

body,html {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}

</style>
