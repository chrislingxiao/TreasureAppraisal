<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationBarTitleText: '收藏家信息',
  },
}
</route>

<template>
  <view class="user">
    <view class="img-block">
      <wd-img custom-class="user-img" :src="joy" mode="widthFix" />
      <view class="user-info py-2">
        <view class="flex flex-col justify-center items-center">
          <text class="user-name mb-2">张老板</text>
          <view class="tags mb-2 flex justify-around">
            <wd-tag type="primary" mark>真滴准</wd-tag>
            <wd-tag type="primary" mark>城里银</wd-tag>
            <wd-tag type="primary" mark>持久霸</wd-tag>
          </view>
        </view>
        <view class="user-description px-2">
          持久力强 持久力强 持久力强 持久力强 持久力强 持久力强 持久力强持久力强 持久力强
        </view>
      </view>
    </view>
    <view class="appraisal-count">
      <wd-cell-group border>
        <wd-cell title="已鉴定" center size="large">
          <wd-count-to
            type="error"
            :startVal="0"
            :endVal="888888"
            color="#ff5722"
            :fontSize="28"
            suffix="件"
          ></wd-count-to>
        </wd-cell>
        <wd-cell title="鉴定经验" center size="large">
          <wd-text text="12" type="primary" suffix="年" :lines="2" size="26px" />
          <wd-text></wd-text>
        </wd-cell>
      </wd-cell-group>
    </view>
    <view class="appraisal-list">
      <wd-segmented :options="list" v-model:value="current" size="large"></wd-segmented>
      <view v-if="current === '我是用户'">
        <itemListComp />
      </view>
      <view v-else><itemListComp /></view>
    </view>
  </view>
</template>

<script lang="ts" setup>
import itemListComp from '../components/itemList.vue'

const joy =
  'https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg'

const list = ref<string[]>(['已鉴定', '待鉴定'])
const current = ref('已鉴定')
</script>

<style lang="scss" scoped>
:deep(.user-img) {
  width: 100%;
  height: 100%;
}
:deep(.wd-tag) {
  font-size: medium;
}
.user-info {
  position: absolute;
  top: 280px;
  color: white;
  background-color: grey;
  opacity: 0.9;
}
.user-name {
  font-size: large;
}
.user-description {
  font-size: small;
}
.tags {
  width: 80%;
}
</style>
