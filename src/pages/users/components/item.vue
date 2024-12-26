<route lang="json5">
{
  layout: 'default',
  style: {
    navigationBarTitleText: 'item',
  },
}
</route>

<template>
  <wd-badge :modelValue="itemData.res" :type="resType">
    <view class="item-container flex flex-col">
      <wd-img custom-class="item-img" :src="itemData.pic" mode="widthFix" radius="12"></wd-img>
      <view class="item-name mb-1">
        <wd-text size="16px" :text="itemData.name"></wd-text>
      </view>
      <view class="item-tags">
        <wd-tag
          custom-class="ml-2"
          type="primary"
          v-for="(tag, idx) in itemData.tags"
          :key="idx"
          mark
        >
          {{ tag }}
        </wd-tag>
      </view>
    </view>
  </wd-badge>
</template>

<script lang="ts" setup>
import _ from 'lodash'

const props = defineProps(['item'])
const itemData = props.item
const resType = computed(() => {
  if (_.isNil(itemData.isFake)) {
    return 'warning'
  } else {
    return itemData.isFake ? 'red' : 'success'
  }
})
</script>

<style lang="scss" scoped>
:deep(.item-img) {
  width: 100%;
  height: 100%;
}
</style>
