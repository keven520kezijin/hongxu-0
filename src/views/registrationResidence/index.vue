<!-- 居民登记 -->
<template>
  <div class="registrationResidence">
    <div class="f-s-c">
      <h3>居民登记</h3>
      <a-button type="primary">批量导入</a-button>
    </div>
    <a-divider />
    <template>
      <a-form
        :form="form"
        :label-col="labelCol"
        :wrapper-col="wrapperCol"
        @submit="handleSubmit"
      >
        <div class="bd-hox">
          <a-form-item label="所属小区">
            <template>
              <a-radio-group
                v-decorator="[
                  'radio',
                  { initialValue: 1 },
                  { rules: [{ required: true, message: '请选择所属小区' }] },
                ]"
                name="radioGroup"
              >
                <a-radio :value="1">
                  虹旭小区
                </a-radio>
                <a-radio :value="2">
                  虹旭二小区
                </a-radio>
                <a-radio :value="3">
                  虹警新苑
                </a-radio>
                <a-radio :value="4">
                  中星雅苑
                </a-radio>
              </a-radio-group>
            </template>
          </a-form-item>
          <a-form-item label="房屋">
            <a-input
              v-decorator="[
                'as',
                { rules: [{ required: true, message: '请选择并输入房屋' }] },
              ]"
              placeholder="请选择并输入房屋"
            />
          </a-form-item>
          <a-form-item label="房屋类型">
            <template>
              <a-radio-group
                v-decorator="[
                  'a2',
                  { initialValue: 1 },
                  { rules: [{ required: true, message: '请选择房屋类型' }] },
                ]"
                name="radioGroup"
              >
                <a-radio :value="1">
                  自住
                </a-radio>
                <a-radio :value="2">
                  xxx
                </a-radio>
                <a-radio :value="3">
                  xxx
                </a-radio>
                <a-radio :value="4">
                  xxx
                </a-radio>
              </a-radio-group>
            </template>
          </a-form-item>
        </div>
        <div class="bd-hox">
          <a-form-item label="居名类型">
            <template>
              <a-radio-group
                v-decorator="[
                  'a3',
                  { initialValue: 1 },
                  { rules: [{ required: true, message: '请选择居名类型' }] },
                ]"
                name="radioGroup"
              >
                <a-radio :value="1">
                  业主
                </a-radio>
                <a-radio :value="2">
                  租户
                </a-radio>
                <a-radio :value="3">
                  x x x
                </a-radio>
                <a-radio :value="4">
                  xxx
                </a-radio>
              </a-radio-group>
            </template>
          </a-form-item>
          <a-form-item label="姓名">
            <a-input
              v-decorator="[
                'a4',
                { rules: [{ required: true, message: '请输入姓名' }] },
              ]"
              placeholder="请输入姓名"
            />
          </a-form-item>
          <a-form-item label="头像">
            <template>
              <div class="clearfix">
                <a-upload
                  accept="image/jpeg,image/png"
                  action="https://www.mocky.io/v2/5cc8019d300000980a055e76"
                  list-type="picture-card"
                  :file-list="fileList"
                  @preview="handlePreview"
                  @change="handleChange"
                >
                  <div v-if="fileList.length < 1">
                    <a-icon type="plus" />
                    <div class="ant-upload-text">
                      Upload
                    </div>
                  </div>
                </a-upload>
                <a-modal
                  :visible="previewVisible"
                  :footer="null"
                  @cancel="handleCancel"
                >
                  <img
                    alt="example"
                    style="width: 100%"
                    :src="previewImage"
                  />
                </a-modal>
              </div>
            </template>
          </a-form-item>
          <a-form-item label="出生日期">
            <!-- <a-input
              v-decorator="[
                'a4',
                { rules: [{ required: true, message: '请选择出生日期' }] },
              ]"
              placeholder="请输入姓名"
            /> -->
            <a-date-picker
              v-decorator="[
                'a5',
                { rules: [{ required: true, message: '请选择出生日期' }] },
              ]"
              :format="dateFormat"
            />
          </a-form-item>
        </div>
        <a-form-item :wrapper-col="{ span: 12, offset: 6 }">
          <a-button
            type="primary"
            html-type="submit"
          >
            Submit
          </a-button>
        </a-form-item>
      </a-form>
    </template>
  </div>
</template>

<script>
import moment from 'moment'
function getBase64 (file) {
  return new Promise((resolve, reject) => {
    const reader = new FileReader()
    reader.readAsDataURL(file)
    reader.onload = () => resolve(reader.result)
    reader.onerror = error => reject(error)
  })
}
export default {
  components: {},
  data () {
    return {
      labelCol: {
        xs: { span: 24 },
        sm: { span: 2 }
      },
      wrapperCol: {
        xs: { span: 24 },
        sm: { span: 12 }
      },
      // dateFormat: 'YYYY/MM/DD', // 日期格式
      previewVisible: false, // 预览model
      previewImage: '', // 预览图片地址
      fileList: [
        {
          uid: '-3',
          name: 'image.png',
          status: 'done',
          url: 'https://zos.alipayobjects.com/rmsportal/jkjgkEfvpUPVyRjUImniVslZfWPnJuuZ.png'
        }
      ]
    }
  },
  computed: {},
  watch: {},
  created () {

  },
  mounted () {

  },
  beforeCreate () {
    this.form = this.$form.createForm(this)
  },
  beforeMount () { },
  beforeUpdate () { },
  updated () { },
  beforeDestroy () { },
  destroyed () { },
  activated () { },
  methods: {
    moment,
    handleSubmit (e) {
      e.preventDefault()
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values)
        }
      })
    },
    handleCancel () {
      this.previewVisible = false
    },
    async handlePreview (file) {
      if (!file.url && !file.preview) {
        file.preview = await getBase64(file.originFileObj)
      }
      this.previewImage = file.url || file.preview
      this.previewVisible = true
    },
    handleChange ({ fileList }) {
      this.fileList = fileList
    }
  }
}
</script>
<style lang='less' scoped>
//@import url(); 引入公共css类
.registrationResidence {
  background: #fff;
  padding: 20px 40px;
}
ant-upload-select-picture-card i {
  font-size: 32px;
  color: #999;
}

.ant-upload-select-picture-card .ant-upload-text {
  margin-top: 8px;
  color: #666;
}
</style>
