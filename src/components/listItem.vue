<route lang="json5">
{
  layout: 'default',
  style: {
    navigationBarTitleText: 'list',
  },
}
</route>

<template>
  <view class="category-item border-rounded-lg p4 mb-1">
    <view class="content flex justify-between mb-2">
      <wd-img
        :key="idx"
        :width="80"
        :height="80"
        :src="pic"
        :radius="6"
        lazy-load
        v-for="(pic, idx) in itemData.pic"
      />
    </view>
    <view class="comments">
      <wd-cell-group>
        <wd-cell
          :key="idx"
          :title="data.name"
          :value="data.content"
          v-for="(data, idx) in itemData.comments"
        />
      </wd-cell-group>
    </view>
  </view>
</template>

<script lang="ts" setup>
const props = defineProps(['item'])
const itemData = props.item
</script>

<style lang="scss" scoped>
//
.category-item {
  background-color: rgb(240, 239, 239);
}
</style>
