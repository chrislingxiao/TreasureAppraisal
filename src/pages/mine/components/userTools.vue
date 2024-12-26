<route lang="json5">
{
  layout: 'default',
  style: {
    navigationBarTitleText: '',
  },
}
</route>

<template>
  <view class="user-tools mt-2">
    <wd-toast />

    <wd-cell-group border>
      <wd-cell title="我的鉴定" is-link to="/pages/mine/pages/appraisalList" size="large"></wd-cell>
      <wd-cell title="我的偷看" is-link to="/pages/testpage/index" size="large"></wd-cell>
      <wd-cell title="我的收益" is-link to="/pages/testpage/index" size="large"></wd-cell>
      <wd-cell title="我的消费" is-link to="/pages/testpage/index" size="large"></wd-cell>
      <wd-cell title="点击测试" size="large" clickable @click="showToast"></wd-cell>
    </wd-cell-group>
  </view>
</template>

<script lang="ts" setup>
import { useToast } from 'wot-design-uni'
const toast = useToast()

const showToast = () => {
  toast.show('点击')
}
</script>

<style lang="scss" scoped>
//
</style>
