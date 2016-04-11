<template lang="jade">
.container
  a(href="https://github.com/vue-comps/vue-pushpin/blob/master/dev/basic.vue") source
  pushpin(:offset="200",:top="400",:bottom="400")
    p content
  p make the window small (height &lt; 800px) and scroll to the bottom
</template>

<script lang="coffee">
module.exports =
  components:
    "pushpin": require "../src/pushpin.vue"
</script>

<style lang="stylus">
.container > a
  position absolute
  left 250px
  top 40px
  height 2000px
</style>
