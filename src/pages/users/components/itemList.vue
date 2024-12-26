<route lang="json5">
{
  layout: 'default',
  style: {
    navigationBarTitleText: '',
  },
}
</route>

<template>
  <view class="item-list">
    <wd-grid :gutter="12" :column="2">
      <wd-grid-item v-for="(item, idx) in list" :key="idx" use-slot>
        <ItemComp :item="item"></ItemComp>
      </wd-grid-item>
    </wd-grid>
  </view>
</template>

<script lang="ts" setup>
import ItemComp from './item.vue'

const list = []

for (let i = 0; i < 6; i++) {
  const item = {
    pic: 'https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg',
    name: '牛逼的东西',
    tags: ['123', '123', '123'],
    res: '真',
    isFake: false,
  }
  if (i === 2 || i === 4) {
    item.isFake = true
    item.res = '赝'
  } else if (i === 3) {
    item.isFake = null
    item.res = '疑'
  }
  list.push(item)
}
</script>

<style lang="scss" scoped>
//
</style>
