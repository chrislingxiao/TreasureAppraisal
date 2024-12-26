<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationBarTitleText: '专家申请',
  },
}
</route>

<template>
  <view class="bg-white overflow-hidden mt-2 px-4">
    <!-- <wd-navbar left-text="返回" left-arrow @click-left="handleClickLeft"></wd-navbar> -->

    <wd-message-box />
    <wd-toast />

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

    <wd-message-box selector="policy-check" />

    <wd-form ref="form" :model="model" :rules="rules">
      <wd-cell-group custom-class="group" title="个人信息" border>
        <wd-cell title="本人照片" title-width="100px" prop="userImages">
          <wd-upload
            accept="image"
            :file-list="model.userImages"
            :limit="3"
            :action="action"
            @change="handleFileChange"
          ></wd-upload>
        </wd-cell>
        <wd-cell
          custom-class="id-images"
          title="身份证(正反两张)"
          title-width="100px"
          prop="idImages"
        >
          <view class="flex flex-col">
            <wd-upload
              accept="image"
              :file-list="model.idImages"
              :limit="2"
              :action="action"
              @change="handleFileChange"
            ></wd-upload>
            <wd-button type="text" @click="checkExample">查看示例</wd-button>
          </view>
        </wd-cell>
        <wd-textarea
          label="个人简介"
          label-width="100px"
          v-model="model.description"
          placeholder="请填写个人简介"
        />
        <wd-cell title="擅长领域" title-width="70px" prop="idImages">
          <wd-checkbox-group v-model="model.focusParts" cell shape="button">
            <wd-checkbox modelValue="1">选项</wd-checkbox>
            <wd-checkbox modelValue="2">选项</wd-checkbox>
            <wd-checkbox modelValue="3">选项</wd-checkbox>
            <wd-checkbox modelValue="4">选项</wd-checkbox>
            <wd-checkbox modelValue="5">选项</wd-checkbox>
            <wd-checkbox modelValue="6">选项</wd-checkbox>
            <wd-checkbox modelValue="7">选项</wd-checkbox>
            <wd-checkbox modelValue="8">选项</wd-checkbox>
            <wd-checkbox modelValue="9">选项</wd-checkbox>
          </wd-checkbox-group>
        </wd-cell>
        <wd-input
          label="邀请码"
          label-width="100px"
          v-model="model.inviteCode"
          placeholder="请输入邀请码..."
          clear-trigger="focus"
          clearable
        ></wd-input>
      </wd-cell-group>
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
      <view class="footer">
        <wd-button type="primary" size="large" @click="handleSubmit" :block="isDisabled">
          提交
        </wd-button>
      </view>
    </wd-form>
  </view>
</template>

<script lang="ts" setup>
// form setup
import { useToast, useMessage } from 'wot-design-uni'
import { isArray } from 'wot-design-uni/components/common/util'
import { FormRules } from 'wot-design-uni/components/wd-form/types'
import { reactive, ref } from 'vue'

const toast = useToast()
const checkExamplePopup = useMessage('example-check')
const checkPolicyPopup = useMessage('policy-check')

const action: string =
  'https://mockapi.eolink.com/zhTuw2P8c29bc981a741931bdd86eb04dc1e8fd64865cb5/upload'

let policyRead: boolean = false

const isDisabled: boolean = true

const model = reactive<{
  userImages: Record<string, string>[]
  idImages: Record<string, string>[]
  description: string
  focusParts: Record<number, number>[]
  inviteCode: number
  read: boolean
}>({
  userImages: [],
  idImages: [],
  description: '',
  focusParts: [],
  inviteCode: null,
  read: false,
})

const rules: FormRules = {
  userImages: [
    {
      required: true,
      message: '请上传个人正面照',
      validator: (value) => {
        if (isArray(value) && value.length) {
          return Promise.resolve()
        } else {
          // eslint-disable-next-line prefer-promise-reject-errors
          return Promise.reject()
        }
      },
    },
  ],
  idImages: [
    {
      required: true,
      message: '请上传身份证',
      validator: (value) => {
        if (isArray(value) && value.length) {
          return Promise.resolve()
        } else {
          // eslint-disable-next-line prefer-promise-reject-errors
          return Promise.reject()
        }
      },
    },
  ],
  description: [
    {
      required: true,
      message: '请输入个人简单介绍',
      validator: (value) => {
        if (value && value.length > 2) {
          return Promise.resolve()
        } else {
          // eslint-disable-next-line prefer-promise-reject-errors
          return Promise.reject('请输入个人简单介绍')
        }
      },
    },
  ],
  focusParts: [
    {
      required: true,
      message: '请选择鉴宝领域',
      validator: (value) => {
        if (value && value.length > 0) {
          return Promise.resolve()
        } else {
          // eslint-disable-next-line prefer-promise-reject-errors
          return Promise.reject('请选择鉴宝领域')
        }
      },
    },
  ],
}

const form = ref()

function handleFileChange({ fileList }) {
  model.userImages = fileList
  model.idImages = fileList
}

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

// const handleClickLeft = () => {
//   uni.navigateBack({
//     delta: 1,
//   })
// }

const handlePolicyChange = ({ value }) => {
  policyRead = value
}

const checkExample = () => {
  checkExamplePopup.alert({
    title: '身份证样例',
  })
}

const checkPolicy = () => {
  checkPolicyPopup.alert({
    title: '牛逼银协议',
    msg: '都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌都是牛逼银都是大屌',
  })
}
</script>

<style lang="scss" scoped>
.tip {
  margin: 10px 15px 21px;
  font-size: 12px;
  color: #999;
}
.footer {
  padding: 0 25px 21px;
}
:deep(.label-class) {
  font-size: 12px !important;
  color: #999 !important;
}
</style>
