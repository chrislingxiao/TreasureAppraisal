<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationBarTitleText: 'test page',
  },
}
</route>

<template>
  <view>
    <view
      class="bg-white overflow-hidden pt-2 px-4"
      :style="{ marginTop: safeAreaInsets?.top + 'px' }"
    >
      <view class="text-center text-3xl mt-8">
        兄弟们好，我们是
        <text class="text-red-500">王大屌和张大屌</text>
      </view>
      <RequestComp />
      <UploadComp />
    </view>
  </view>
</template>

<script lang="ts" setup>
const { safeAreaInsets } = uni.getSystemInfoSync()

const handleClickLeft = () => {
  uni.navigateBack()
}

onLoad(() => {
  uni.setNavigationBarTitle({
    title: '牛逼银儿',
  })
})
</script>

<style lang="scss" scoped>
//
</style>
