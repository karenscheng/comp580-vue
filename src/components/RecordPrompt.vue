<template>
<div class = "recordprompt">
  <h1>will play once you press a key, asshole</h1>
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
