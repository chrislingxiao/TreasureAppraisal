<route lang="json5">
{
  style: {
    navigationBarTitleText: '鉴宝申请',
  },
}
</route>

<template>
  <wd-toast />
  <wd-message-box selector="policy-check" />
  <wd-message-box selector="example-check">
    <view>
      <wd-img
        style="width: 100%; height: 150px"
        radius="6"
        src="https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg"
      />
      <wd-img
        style="width: 100%; height: 150px"
        radius="6"
        src="https://img11.360buyimg.com/imagetools/jfs/t1/143248/37/5695/265818/5f3a8546E98d998a4/745897ca9c9e474b.jpg"
      />
    </view>
  </wd-message-box>
  <wd-form ref="form" :model="model">
    <wd-cell-group border>
      <wd-picker
        :columns="categories"
        label="藏品分类"
        label-width="100px"
        v-model="model.category"
        :rules="[{ required: true, message: '请选择藏品类别' }]"
      />
      <wd-textarea
        label="藏品描述"
        label-width="100px"
        v-model="model.description"
        placeholder="请填写藏品描述"
        :rules="[{ required: true, message: '请填写藏品描述' }]"
      />
      <wd-cell
        custom-class="id-images"
        title="藏品照片(正反两张)"
        title-width="100px"
        prop="images"
        :rules="[{ required: true, message: '请上传藏品照片' }]"
      >
        <view class="flex flex-col">
          <wd-upload
            accept="image"
            :file-list="model.images"
            :limit="2"
            :action="action"
            @change="handleFileChange"
          ></wd-upload>
          <wd-button type="text" @click="checkExample">查看示例</wd-button>
        </view>
      </wd-cell>
      <wd-picker
        :columns="appraisalTypes"
        label="鉴定类型"
        label-width="100px"
        v-model="model.appraisalType"
        :rules="[{ required: true, message: '请选择鉴定类型' }]"
      />
      <wd-cell custom-class="id-images" title="鉴定价格" title-width="100px">
        <view class="summary">
          <wd-text :text="price" mode="price" type="success" prefix="￥" size="24px" />
        </view>
      </wd-cell>

      <view class="tip">
        <wd-checkbox
          v-model="policyRead"
          prop="read"
          custom-label-class="label-class"
          @change="handlePolicyChange"
        >
          已阅读并同意
          <wd-text text="《牛逼银协议》" @click="checkPolicy" style="color: #4d80f0"></wd-text>
        </wd-checkbox>
      </view>
    </wd-cell-group>

    <view class="footer mt-2">
      <wd-button type="primary" size="large" @click="handleSubmit" block>提交</wd-button>
    </view>
  </wd-form>
</template>

<script lang="ts" setup>
import { useMessage, useToast } from 'wot-design-uni'
const toast = useToast()

const checkExamplePopup = useMessage('example-check')
const checkPolicyPopup = useMessage('policy-check')

let policyRead: boolean = false

const categories = ref([
  ['牛逼', '假牛逼', '真牛逼'],
  ['哈哈哈哈', '嘻嘻嘻嘻嘻', '哇哈哈哇哈哈'],
])
const appraisalTypes = ref(['一人', '专家组'])

const action: string =
  'https://mockapi.eolink.com/zhTuw2P8c29bc981a741931bdd86eb04dc1e8fd64865cb5/upload'

const model = reactive<{
  description: string
  category: Array<string>
  images: Record<string, string>[]
  appraisalType: string
}>({
  description: '',
  category: [],
  images: [],
  appraisalType: '',
})

const form = ref()

const price = computed(() => {
  if (!model.appraisalType) {
    return '0.00'
  }
  return model.appraisalType === '一人' ? '15' : '30'
})

function handleSubmit() {
  if (!policyRead) {
    toast.warning('请同意policy')
  } else {
    form.value
      .validate()
      .then(({ valid, errors }) => {
        console.log(valid)
        console.log(errors)
      })
      .catch((error) => {
        console.log(error, 'error')
      })
  }
}

function handleFileChange({ fileList }) {
  model.images = fileList
}
const handlePolicyChange = ({ value }) => {
  policyRead = value
}
function checkExample() {
  checkExamplePopup.alert({
    title: '藏品照片样例',
  })
}
function checkPolicy() {
  checkPolicyPopup.alert({
    title: '牛逼银协议',
    msg: '都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌',
  })
}
</script>

<style lang="scss" scoped>
.test-css {
  // mt-4=>1rem=>16px;
  margin-top: 16px;
}
.tip {
  margin: 10px 15px 21px;
  font-size: 12px;
  color: #999;
}
:deep(.label-class) {
  font-size: 12px !important;
  color: #999 !important;
}
</style>
