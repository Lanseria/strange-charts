<script lang="ts" setup>
import type { CSSProperties } from 'vue'
const props = defineProps({
  width: {
    type: Number,
    default: 126,
  },
  strokeWidth: {
    type: Number,
    default: 6,
  },
  color: {
    type: [String, Function],
    default: '#63a26c',
  },
  percentage: {
    type: Number,
    default: 0,
  },
  strokeLinecap: {
    type: String,
    default: 'round',
  },
})
const relativeStrokeWidth = computed(() =>
  ((props.strokeWidth / props.width) * 100).toFixed(1),
)
const radius = computed(() => {
  return Number.parseInt(
          `${50 - Number.parseFloat(relativeStrokeWidth.value) / 2}`,
          10,
  )
})
const perimeter = computed(() => 2 * Math.PI * radius.value)
const trackPath = computed(() => {
  const r = radius.value
  const isDashboard = false
  return `
          M 50 50
          m 0 ${isDashboard ? '' : '-'}${r}
          a ${r} ${r} 0 1 1 0 ${isDashboard ? '-' : ''}${r * 2}
          a ${r} ${r} 0 1 1 0 ${isDashboard ? '' : '-'}${r * 2}
          `
})
const rate = computed(() => 1)
const strokeDashoffset = computed(() => {
  const offset = (-1 * perimeter.value * (1 - rate.value)) / 2
  return `${offset}px`
})

const trailPathStyle = computed(
  (): CSSProperties => ({
    strokeDasharray: `${perimeter.value * rate.value}px, ${
          perimeter.value
        }px`,
    strokeDashoffset: strokeDashoffset.value,
  }),
)
const getCurrentColor = (percentage: number) => {
  const { color } = props
  if (typeof color === 'function')
    return color(percentage)

  if (typeof color === 'string')
    return color
}
const stroke = computed(() => {
  return getCurrentColor(props.percentage)
})

const circlePathStyle = computed(
  (): CSSProperties => ({
    strokeDasharray: `${
          perimeter.value * rate.value * (props.percentage / 100)
        }px, ${perimeter.value}px`,
    strokeDashoffset: strokeDashoffset.value,
    transition: 'stroke-dasharray 0.6s ease 0s, stroke 0.6s ease',
  }),
)
</script>
<template>
  <div
    :style="{ height: `${width}px`, width: `${width}px` }"
  >
    <svg viewBox="0 0 100 100">
      <path
        class="el-progress-circle__track"
        :d="trackPath"
        stroke="#323232"
        :stroke-width="relativeStrokeWidth"
        fill="none"
        :style="trailPathStyle"
      />
      <path
        class="el-progress-circle__path"
        :d="trackPath"
        :stroke="stroke"
        fill="none"
        :stroke-linecap="strokeLinecap"
        :stroke-width="percentage ? relativeStrokeWidth : 0"
        :style="circlePathStyle"
      />
    </svg>
  </div>
</template>
<style lang="css" scoped>

#svg circle {
  stroke-dashoffset: 0;
  transition: stroke-dashoffset 1s linear;
  stroke: #666;
  stroke-width: 1em;
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
