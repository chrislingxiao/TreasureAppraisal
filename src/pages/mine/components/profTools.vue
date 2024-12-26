<route lang="json5">
{
  layout: 'default',
  style: {
    navigationBarTitleText: '',
  },
}
</route>

<template>
  <view class="prof-tools mt-2">
    <wd-toast />
    <view v-if="!isProf" class="flex justify-center mt-10">
      <wd-button size="large" @click="profApply">申请专家</wd-button>
    </view>

    <wd-cell-group v-else border>
      <wd-cell title="待鉴定" is-link to="../testpage/index" size="large"></wd-cell>
      <wd-cell title="已鉴定" is-link to="../testpage/index" size="large"></wd-cell>
      <wd-cell title="我的收益" is-link to="../testpage/index" size="large"></wd-cell>
      <wd-cell title="行家数据" is-link to="../testpage/index" size="large"></wd-cell>
      <wd-cell title="我的银行卡" is-link to="../testpage/index" size="large"></wd-cell>
    </wd-cell-group>
  </view>
</template>

<script lang="ts" setup>
const isProf = computed(() => {
  return false
})

const profApply = () => {
  uni.navigateTo({
    url: './pages/profRegister',
  })
}
</script>

<style lang="scss" scoped>
//
</style>
