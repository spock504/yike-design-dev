<template>
  <yk-form ref="formRef" :model="form" :rules="rulesMap">
    <yk-form-item label="姓名" field="name" :rules="nameExtraRule">
      <yk-input v-model="form.name"></yk-input>
    </yk-form-item>
    <yk-form-item label="昵称" field="nickname">
      <yk-input v-model="form.nickname" placeholder="请输入"></yk-input>
    </yk-form-item>
    <yk-form-item label="性别" field="sex" :rules="rulesMap.sex">
      <yk-radio-group v-model="form.sex">
        <yk-radio value="man">男</yk-radio>
        <yk-radio value="woman">女</yk-radio>
      </yk-radio-group>
    </yk-form-item>
    <yk-form-item label="年龄" field="sex" :rules="rulesMap.sex">
      <yk-input-number v-model="form.age"></yk-input-number>
    </yk-form-item>
    <yk-form-item label="日期" field="date" :required="true">
      <yk-checkbox-group v-model="form.date">
        <yk-checkbox v-for="item in data" :key="item.id" :value="item.id">
          {{ item.label }}
        </yk-checkbox>
      </yk-checkbox-group>
    </yk-form-item>
    <yk-form-item>
      <yk-space>
        <yk-button type="primary" @click="resetForm(formRef)">重置</yk-button>
        <yk-button @click="submitForm(formRef)">提交</yk-button>
      </yk-space>
    </yk-form-item>
  </yk-form>
</template>
<script lang="ts" setup>
import { reactive, ref } from 'vue'
const formRef = ref()
const form = reactive({
  name: '大飞',
  sex: 'man',
  date: ['2'],
  nickname: '',
  age: 20,
})
const rulesMap = {
  name: [
    {
      required: true,
      message: 'Please select Activity count',
      trigger: 'change',
    },
    {
      minLength: 4,
      trigger: 'change',
    },
  ],
  nickname: [
    {
      required: true,
      message: '请输入昵称',
      trigger: 'blur',
    },
  ],
  sex: [
    {
      required: true,
      message: 'Please select Activity count',
    },
  ],
}
const nameExtraRule = [
  {
    maxLength: 6,
    require: true,
    trigger: ['change', 'blur', 'focus'],
  },
]
const data = ref([
  { id: '1', label: '昨天' },
  { id: '2', label: '今天' },
  { id: '3', label: '明天' },
])
const resetForm = (formEl) => {
  if (!formEl) {
    return
  }
  formEl.resetFields()
  console.log('reset')
}
const submitForm = (formEl) => {
  if (!formEl) {
    return
  }
  formEl.validate((errors: any) => {
    console.log(errors)
  })
}
</script>
