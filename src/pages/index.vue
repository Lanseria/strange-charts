<script setup lang="ts">
const ageData = [
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
    name: '95后',
    value: 0.826,
  },
  {
    name: '00后',
    value: 0.735,
  },
]
const houseData = [
  {
    name: '和对象一起住',
    value: 0.865,
  },
  {
    name: '独居',
    value: 0.841,
  },
  {
    name: '和陌生人合租',
    value: 0.805,
  },
  {
    name: '和朋友合租',
    value: 0.783,
  },
  {
    name: '和爸妈一起住',
    value: 0.779,
  },
]
const sexData = [
  {
    name: '男',
    value: 0.842,
  },
  {
    name: '女',
    value: 0.774,
  },
]
</script>

<template>
  <div relative m="auto" md:max-w-175 text-left>
    <div text-2xl mb-10>
      2022疫情囤货小报告：我们看了1412个人的家
    </div>
    <div text-lg>
      谁在囤货？
    </div>
    <p>
      曾经说起“囤货”，大家会觉得这是老一辈人/囤积癖/购物狂们/末日准备者们才有的习惯。毕竟，这是一个消费品随处可得的时代。
    </p>
    <p>
      但在最近一波疫情中，越来越多人居家隔离，也就越来越多人选择囤货。在参与调研的读者中，有超过8成人最近因为疫情而囤货。
    </p>
    <p>
      从年龄来看，从00后到80后，年纪越大，囤货的意愿越大。
    </p>
    <p>
      80后的囤货人数占比是所有人群中最高，达到了85.1%。00后们囤货意识就弱一些，只有73.5%的人为居家隔离做了囤货的准备，有接近3成人都没囤。
    </p>
    <div mt-4 grid grid-cols-2 gap-15 place-items-center>
      <chart-one :data="ageData" title="年龄" />
      <chart-one :data="houseData" title="居住状况" />
      <chart-one :data="sexData" title="性别" />
    </div>
  </div>
</template>
