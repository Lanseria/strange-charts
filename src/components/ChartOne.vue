<script lang="ts" setup>
const datas = [
  {
    name: '80后',
    value: 0.851,
  },
  {
    name: '85后',
    value: 0.84,
  },
  {
    name: '90后',
    value: 0.834,
  },
  {
    name: '00后',
    value: 0.735,
  },
]
</script>
<template>
  <ProcessCircle :val="60" />
</template>
<style lang="css" scoped>

</style>
