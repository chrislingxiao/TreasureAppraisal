<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationBarTitleText: '我的鉴定',
  },
}
</route>

<template>
  <view class="my-appraisal px-4">
    <ListItemComp :item="item" v-for="(item, idx) in list" :key="idx" />
  </view>
</template>

<script lang="ts" setup>
import ListItemComp from '@/components/listItem.vue'

const list = []
for (let i = 0; i < 30; i++) {
  list.push({
    pic: [
      'https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg',
      'https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg',
      'https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg',
      'https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg',
    ],
    comments: [
      {
        name: '张老板',
        content: '真牛逼',
      },
      {
        name: '王老板',
        content: '太牛逼',
      },
    ],
  })
}
</script>

<style lang="scss" scoped>
//
</style>
