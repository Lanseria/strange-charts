<script lang="ts" setup>
const props = defineProps({
  val: {
    type: Number,
    required: true,
  },
})
let { val } = props
const r = $ref(90)
const c = $ref(Math.PI * (r * 2))

if (val < 0)
  val = 0
if (val > 100)
  val = 100

const offsetPx = computed(() => {
  return ((100 - val) / 100) * c
})
</script>
<template>
  <svg id="svg" width="200" height="200" viewPort="0 0 100 100" version="1.1" xmlns="http://www.w3.org/2000/svg">
    <circle :r="r" cx="100" cy="100" fill="transparent" stroke-dasharray="565.48" stroke-dashoffset="0" />
    <circle
      id="bar" :r="r" cx="100" cy="100" fill="transparent" stroke-dasharray="565.48" stroke-dashoffset="0" :style="{
        strokeDashoffset: offsetPx + 'px'
      }"
    />
  </svg>
</template>
<style lang="css" scoped>

#svg circle {
  stroke-dashoffset: 0;
  transition: stroke-dashoffset 1s linear;
  stroke: #666;
  stroke-width: 1em;
}
#svg #bar {
  stroke: #FF9F1E;
}
#cont {
  display: block;
  height: 200px;
  width: 200px;
  margin: 2em auto;
  box-shadow: 0 0 1em black;
  border-radius: 100%;
  position: relative;
}
#cont:after {
  position: absolute;
  display: block;
  height: 160px;
  width: 160px;
  left: 50%;
  top: 50%;
  box-shadow: inset 0 0 1em black;
  margin-top: -80px;
  margin-left: -80px;
  border-radius: 100%;
  line-height: 160px;
  font-size: 2em;
  text-shadow: 0 0 0.5em black;
}
</style>
