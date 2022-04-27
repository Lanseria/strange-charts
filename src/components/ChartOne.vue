<script lang="ts" setup>
import type { PropType } from 'vue'

interface NameValue {
  name: string
  value: number
}
const props = defineProps({
  data: {
    type: Array as PropType<NameValue[]>,
    default: () => [],
  },
  title: {
    type: String,
    default: '',
  },
})
const formatData = computed(() => {
  if (props.data.length > 5) {
    return props.data.slice(0, 5)
  }
  else if (props.data.length === 5) {
    return props.data
  }
  else {
    const restCount = 5 - props.data.length
    const restData = Array(restCount).fill({
      name: '',
      value: 0,
    })
    return [...props.data, ...restData]
  }
})
</script>
<template>
  <div relative w-full h-50>
    <div absolute bottom="-4" left-25 z-1 p="x-3 y-0.5" bg-gray-900 b-gray-50 border class="title">
      {{ title }}
    </div>
    <ProcessCircle
      v-for="(item,idx) in formatData" :key="idx" transform="scale-x-[-1]" absolute :percentage="item.value * 100" :stroke-width="10" :width="(200-idx*40)" :color="idx<2?'#63a26c':'#aab9af'" :style="{
        top: `${idx*20}px`,
        left: `${idx*20}px`,
      }"
    />
    <div class="text-desc" absolute left="25" top="-1" p="l2">
      <div v-for="(item,idx) in formatData" :key="idx" class="item-desc" text-sm>
        <span
          :class="{
            'font-bold':idx<2
          }"
        >{{ item.name }}</span>
        <span v-if="item.value" m="l2">{{ (item.value * 100).toFixed(1) }}%</span>
      </div>
    </div>
  </div>
</template>
<style lang="css" scoped>

</style>
