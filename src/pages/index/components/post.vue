<route lang="json5">
{
  layout: 'default',
  style: {
    navigationBarTitleText: 'post',
  },
}
</route>

<template>
  <view class="post-card border-rounded-lg p4 mb-1">
    <view class="title flex justify-start mb-2" @click="toUserPage">
      <wd-img
        src="https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg"
        width="50"
        height="50"
        alt="joy"
        style="margin-right: 12px"
        round
      />
      <view class="flex flex-col justify-center justify-items-center">
        <view style="font-size: 16px; color: rgba(0, 0, 0, 0.85)">牛逼银</view>
        <view style="font-size: 12px; color: rgba(0, 0, 0, 0.25)">高级版-快速吸粉 | 周期一年</view>
      </view>
    </view>
    <view class="content flex justify-between mb-2">
      <wd-img :width="100" :height="100" :src="joy" :radius="6" lazy-load />
      <wd-img :width="100" :height="100" :src="joy" :radius="6" lazy-load />
      <wd-img :width="100" :height="100" :src="joy" :radius="6" lazy-load />
    </view>
    <view class="comments">
      <wd-cell-group>
        <wd-cell title="张老板:" value="真叼" />
        <wd-cell title="王老板:" value="应该是假叼" />
      </wd-cell-group>
    </view>
  </view>
</template>

<script lang="ts" setup>
// 测试 uni API 自动引入
const joy =
  'https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg'

onLoad(() => {
  console.log('posts loaded')
})

function toUserPage() {
  uni.navigateTo({
    url: '../users/pages/users',
  })
}
</script>

<style lang="scss" scoped>
//
.post-card {
  background-color: rgb(240, 239, 239);
}
</style>
