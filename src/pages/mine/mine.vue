<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationBarTitleText: '我的',
  },
}
</route>

<template>
  <view class="bg-white overflow-hidden mt-2 px-4">
    <view class="user-card border-rounded-lg p4 mb-1">
      <view class="title flex justify-start align-center mb-2">
        <wd-img
          src="https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg"
          width="50"
          height="50"
          alt="joy"
          style="margin-right: 12px"
          round
        />
        <view class="flex flex-col justify-center justify-items-center pl-2">
          <view>张老板</view>
          <view class="flex flex-row color-bluegray user-info">
            <view class="mr-2">1k关注</view>
            <view>2k关注我</view>
          </view>
        </view>
      </view>
    </view>
    <view class="user-assets-card border-rounded-lg py4 mb-1">
      <wd-segmented :options="list" v-model:value="current" size="large"></wd-segmented>
      <view v-if="current === '我是用户'">
        <UserToolsComp />
      </view>
      <view v-else>
        <ProfToolsComp />
      </view>
    </view>
  </view>
</template>

<script lang="ts" setup>
import UserToolsComp from './components/userTools.vue'
import ProfToolsComp from './components/profTools.vue'

const list = ref<string[]>(['我是用户', '我是行家'])

const current = ref('我是用户')

onLoad(() => {
  console.log('posts loaded')
})
</script>

<style lang="scss" scoped>
//
.user-info {
  font-size: small;
}
.user-card {
  background-color: rgb(240, 239, 239);
}
</style>
