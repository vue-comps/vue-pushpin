// out: ..
<template lang="jade">
div(
  v-bind:style="style"
  )
  slot
</template>

<script lang="coffee">
module.exports =

  mixins:[
    require("vue-mixins/onWindowScroll")
  ]

  props:
    "top":
      type: Number
      default: 0
    "offset":
      type: Number
      default: 0
    "bottom":
      type: Number
      default: 0

  data: ->
    style:
      position: null
      top: null
  methods:
    calc: ->
      body = document.body
      html = document.documentElement
      scrollTop = window.pageYOffset or html.scrollTop
      height = document.height or Math.max( body.scrollHeight, body.offsetHeight,html.clientHeight, html.scrollHeight, html.offsetHeight )
      if scrollTop+@offset < @top
        @style.top = @top+ "px"
        @style.position = "absolute"
      else if scrollTop+@offset > height - @bottom
        @style.top = height - @bottom + "px"
        @style.position = "absolute"
      else
        @style.top = @offset + "px"
        @style.position = "fixed"

  compiled: ->
    @onWindowScroll @calc
  attached: ->
    @calc()

</script>
