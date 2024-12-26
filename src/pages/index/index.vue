<!-- 使用 type="home" 属性设置首页，其他页面不需要设置，默认为page；推荐使用json5，更强大，且允许注释 -->
<route lang="json5" type="home">
{
  style: {
    navigationStyle: 'custom',
    navigationBarTitleText: '首页',
  },
}
</route>
<template>
  <view
    class="bg-white overflow-hidden pt-2 px-4"
    :style="{ marginTop: safeAreaInsets?.top + 'px' }"
  >
    <view class="mb-4">
      <wd-search hide-cancel placeholder-left />
    </view>
    <view class="mb-4">
      <wd-swiper
        :list="swiperList"
        autoplay
        v-model:current="current"
        :indicator="{ type: 'dots-bar' }"
        @click="handleClick"
        @change="onChange"
      ></wd-swiper>
    </view>
    <view class="category mb-4">
      <wd-grid :column="4" border>
        <wd-grid-item icon="picture" text="瓷器" @click="() => gotoCategory('瓷器')" />
        <wd-grid-item icon="eye-close" text="钱币" @click="() => gotoCategory('钱币')" />
        <wd-grid-item icon="computer" text="书画" />
        <wd-grid-item icon="filter" text="玉翠珠宝" />
        <wd-grid-item icon="chat" text="金银器" />
        <wd-grid-item icon="camera" text="铜杂" />
        <wd-grid-item icon="note" text="木器家具" />
        <wd-grid-item icon="goods" text="邮卡" />
      </wd-grid>
    </view>
    <wd-divider color="#4D80F0"></wd-divider>
    <view class="caret-rose-5">
      <wd-cell title="实时在线专家数" size="large">
        <view class="online-count">
          <wd-icon name="usergroup"></wd-icon>
          12312311
        </view>
      </wd-cell>
    </view>
    <wd-tabs v-model="tab">
      <block v-for="item in ['最新点评', '最新上传']" :key="item">
        <wd-tab :title="`${item}`">
          <view class="content">
            <PostComp />
            <PostComp />
            <PostComp />
          </view>
        </wd-tab>
      </block>
    </wd-tabs>
    <wd-backtop :scrollTop="scrollTop"></wd-backtop>
  </view>
</template>

<script lang="ts" setup>
import PostComp from './components/post.vue'

// 获取屏幕边界到安全区域距离
const { safeAreaInsets } = uni.getSystemInfoSync()
const author = ref('菲鸽')

const scrollTop = ref<number>(0)
onPageScroll((e) => {
  scrollTop.value = e.scrollTop
})

const tab = ref<number>(0)

defineOptions({
  name: 'Home',
})

// 测试 uni API 自动引入
onLoad(() => {
  console.log(author)
})

const current = ref<number>(0)

const swiperList = ref([
  '../../static/images/cash.png',
  '../../static/images/china1.png',
  '../../static/images/china2.png',
  '../../static/images/coin1.png',
  '../../static/images/coin2.png',
  '../../static/images/painting.png',
])

function handleClick(e) {
  uni.navigateTo({
    url: './pages/categoryList',
  })
}
function onChange(e) {
  console.log(e)
}
function gotoCategory(category) {
  uni.navigateTo({
    url: `./pages/categoryList?category=${category}`,
  })
}
</script>

<style>
.main-title-color {
  color: #d14328;
}
.online-count {
  color: #d14328;
}
</style>
