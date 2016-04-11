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
    require("vue-mixins/getDocumentHeight")
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
      scrollTop = window.pageYOffset or document.documentElement.scrollTop
      if @bottom
        height = @getDocumentHeight()
      if scrollTop+@offset < @top
        @style.top = @top  + "px"
        @style.position = "absolute"
      else if @bottom and scrollTop+@offset > height - @bottom
        @style.top = height - @bottom + "px"
        @style.position = "absolute"
      else if @style.position != "fixed"
        @style.top = @offset + "px"
        @style.position = "fixed"

  compiled: ->
    @onWindowScroll @calc
  attached: ->
    @calc()

</script>
