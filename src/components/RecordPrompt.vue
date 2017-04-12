<template>
<div class = "recordprompt">
  <h1>We will start recording once you start playing! Press Enter to continue!</h1>
</div>
</template>

<script>
export default {
  name: 'recordprompt',
  mounted () {
    window.addEventListener('keydown', this.keyPressed)
  },

  methods: {
    keyPressed (e) {
      this.$emit('start')
    }
  }
}

</script>

<style scoped>

</style>
