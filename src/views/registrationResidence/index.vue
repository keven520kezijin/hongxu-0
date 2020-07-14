<!-- 居民登记 -->
<template>
  <div class="registrationResidence">
    <div class="f-s-c nav-hox">
      <h3>居民登记</h3>
      <a-button type="primary">批量导入</a-button>
    </div>
    <div class="form-hox">
      <template>
        <a-form
          :form="form"
          :label-col="labelCol"
          :wrapper-col="wrapperCol"
          @submit="handleSubmit"
        >
          <a-form-item
            label="所属小区"
            :wrapper-col="radioCol.wrapperCol"
            :label-col="radioCol.labelCol"
          >
            <a-row>
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
            </a-row>

          </a-form-item>
          <a-row>
            <a-col :span="12">
              <!-- <a-col :span='3'></a-col> -->
              <a-form-item
                label="房屋"
                :wrapper-col=" {
                  xs: { span: 24 },
                  sm: { span: 9 }
                }"
                :label-col="{
                  xs: { span: 24 },
                  sm: { span: 14 }
                }"
              >
                <a-select
                  v-decorator="[
                    'ac',
                    { rules: [{ required: true, message: '请选择或输入楼栋号' }] },
                  ]"
                  placeholder="请选择或输入楼栋号"
                >
                  <a-select-option
                    v-for="i in 25"
                    :key="(i + 9).toString(36) + i"
                  >
                    {{ (i + 9).toString(36) + i }}
                  </a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
            <a-col :span="10">
              <a-form-item
                :wrapper-col=" {
                  xs: { span: 24 },
                  sm: { span: 12 }
                }"
                :label-col="{
                  xs: { span: 24 },
                  sm: { span: 0 }
                }"
              >
                <a-select
                  v-decorator="[
                    'ad',
                    { rules: [{ required: true, message: '请选择或输入门牌号' }] },
                  ]"
                  placeholder="请选择或输入门牌号"
                >
                  <a-select-option
                    v-for="i in 25"
                    :key="(i + 9).toString(36) + i"
                  >
                    {{ (i + 9).toString(36) + i }}
                  </a-select-option>
                </a-select>
              </a-form-item>
            </a-col>
          </a-row>
          <a-form-item
            label="房屋类型"
            :wrapper-col="radioCol.wrapperCol"
            :label-col="radioCol.labelCol"
          >
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
                  出租
                </a-radio>
                <a-radio :value="2">
                  自住
                </a-radio>
                <a-radio :value="3">
                  空置
                </a-radio>
              </a-radio-group>
            </template>
          </a-form-item>
          <a-form-item
            label="居名类型"
            :wrapper-col="radioCol.wrapperCol"
            :label-col="radioCol.labelCol"
          >
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
                  家庭常驻人员
                </a-radio>
                <a-radio :value="3">
                  住房租客
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
                      上传照片
                    </div>
                  </div>

                </a-upload>
                <span style="height: 20px;line-height: 20px;">只支持.jpg 格式</span>
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
          <a-form-item
            label="出生日期"
            style="margin-bottom:10px;"
          >
            <a-date-picker
              style="width:100%;"
              v-decorator="[
                'a5',
                { rules: [{ required: true, message: '请选择出生日期' }] },
              ]"
              :format="dateFormat"
            />
          </a-form-item>
          <a-row style="margin-bottom:24px;">
            <a-col :span="7">
            </a-col>
            <a-col
              :span="8"
              class="age-hox"
            >
              <span>年龄: </span>&nbsp;
              <span> - </span>&nbsp;
              <span class="m-l-20">年龄层: </span>
              <span> -</span>
            </a-col>
          </a-row>
          <a-form-item label="身份证号">
            <a-input
              v-decorator="[
                'a6',
                { rules: [{ required: true, message: '请输入身份证号' }] },
              ]"
              placeholder="请输入身份证号"
            />
          </a-form-item>
          <a-form-item label="手机号">
            <a-input
              v-decorator="[
                'a7',
                { rules: [{ required: true, message: '请输入手机号' }] },
              ]"
              placeholder="请输入手机号"
            />
          </a-form-item>
          <a-form-item
            label="文化程度"
            :wrapper-col="radioCol.wrapperCol"
            :label-col="radioCol.labelCol"
          >
            <template>
              <a-radio-group
                v-decorator="[
                  'a8',
                  { initialValue: 1 },
                  { rules: [{ required: true, message: '请选择文化程度' }] },
                ]"
                name="radioGroup"
              >
                <a-radio :value="1">
                  高中以下
                </a-radio>
                <a-radio :value="2">
                  中专
                </a-radio>
                <a-radio :value="3">
                  大专
                </a-radio>
                <a-radio :value="4">
                  本科
                </a-radio>
                <a-radio :value="4">
                  硕士
                </a-radio>
                <a-radio :value="4">
                  博士
                </a-radio>
              </a-radio-group>
            </template>
          </a-form-item>
          <a-row
            id="between"
            v-if="form.getFieldValue('a3')!==2"
          >
            <a-form-item
              label="与户主关系"
              style="color:#f5f5f5;"
              class="aa"
            >
              <a-select
                disabled
                v-decorator="[
                'a9',
              ]"
                placeholder="请选择与户主关系"
              >
                <a-select-option
                  v-for="i in 25"
                  :key="(i + 9).toString(36) + i"
                >
                  {{ (i + 9).toString(36) + i }}
                </a-select-option>
              </a-select>
            </a-form-item>
          </a-row>
          <a-row v-else>
            <a-form-item
              label="与户主关系"
              style="color:#f5f5f5;"
              class="aa"
            >
              <a-select
                v-decorator="[
                'a9',
                { rules: [{ required: true, message: '请选择与户主关系' }] },
              ]"
                placeholder="请选择与户主关系"
              >
                <a-select-option
                  v-for="i in 25"
                  :key="(i + 9).toString(36) + i"
                >
                  {{ (i + 9).toString(36) + i }}
                </a-select-option>
              </a-select>
            </a-form-item>
          </a-row>
          <a-form-item label="户口所在地">
            <a-input
              v-decorator="[
                'a10',
                { rules: [{ required: true, message: '请输入户口所在地' }] },
              ]"
              placeholder="请输入户口所在地"
            />
          </a-form-item>
          <a-form-item label="户口变动日期">
            <a-date-picker
              style="width:100%;"
              v-decorator="[
                'a11',
                { rules: [{ required: false }] },
              ]"
              :format="dateFormat"
            />
          </a-form-item>
          <a-form-item
            label="特殊标签"
            style="margin-bottom: 8px;"
          >
            <a-select
              v-decorator="[
                'a12',
                { rules: [{ required: false }] },
              ]"
              placeholder="请选择特殊标签"
            >
              <a-select-option
                v-for="i in 25"
                :key="(i + 9).toString(36) + i"
              >
                {{ (i + 9).toString(36) + i }}
              </a-select-option>
            </a-select>
          </a-form-item>
          <a-row style="margin-bottom:24px;">
            <a-col :span="7">
            </a-col>
            <a-col :span="17">
              <div>
                <template v-for="(tag) in tagMap">
                  <a-tag
                    closable
                    :key="tag"
                    @close="() => closed(tag)"
                  >
                    {{ tag }}
                  </a-tag>
                </template>
                <a-input
                  v-if="inputVisible"
                  ref="input"
                  type="text"
                  size="small"
                  :style="{ width: '78px' }"
                  :value="inputValue"
                  @change="handleInputChange"
                  @blur="handleInputConfirm"
                  @keyup.enter="handleInputConfirm"
                />
                <a-tag
                  v-else
                  style="background: #fff; borderStyle: dashed;"
                  @click="showInput"
                >
                  <a-icon type="plus" /> 标签
                </a-tag>
              </div>
            </a-col>
          </a-row>
          <a-row>
            <a-col :span="12">
              <a-form-item
                label="户口所在地"
                :wrapper-col=" {
                  xs: { span: 24 },
                  sm: { span: 9 }
                }"
                :label-col="{
                  xs: { span: 24 },
                  sm: { span: 14 }
                }"
              >
                <a-input
                  v-decorator="[
                    'a13',
                    { rules: [{ required: false }] },
                  ]"
                  placeholder="请输入姓名"
                />
              </a-form-item>
            </a-col>
            <a-col :span="10">
              <a-form-item
                :wrapper-col=" {
                  xs: { span: 24 },
                  sm: { span: 12 }
                }"
                :label-col="{
                  xs: { span: 24 },
                  sm: { span: 0 }
                }"
              >
                <a-input
                  v-decorator="[
                    'a14',
                    { rules: [{ required: false }] },
                  ]"
                  placeholder="请输入手机号"
                />
              </a-form-item>
            </a-col>
          </a-row>
          <a-row>
            <a-col :span="12">
              <a-form-item
                label="家庭医生"
                :wrapper-col=" {
                  xs: { span: 24 },
                  sm: { span: 9 }
                }"
                :label-col="{
                  xs: { span: 24 },
                  sm: { span: 14 }
                }"
              >
                <a-input
                  v-decorator="[
                    'a15',
                    { rules: [{ required: false }] },
                  ]"
                  placeholder="请输入姓名"
                />
              </a-form-item>
            </a-col>
            <a-col :span="10">
              <a-form-item
                :wrapper-col=" {
                  xs: { span: 24 },
                  sm: { span: 12 }
                }"
                :label-col="{
                  xs: { span: 24 },
                  sm: { span: 0 }
                }"
              >
                <a-input
                  v-decorator="[
                    'a16',
                    { rules: [{ required: false }] },
                  ]"
                  placeholder="请输入手机号"
                />
              </a-form-item>
            </a-col>
          </a-row>
          <a-form-item label="工作单位">
            <a-input
              v-decorator="[
                'a17',
              ]"
              placeholder="请输入工作单位"
            />
          </a-form-item>
          <a-form-item label="职务">
            <a-input
              v-decorator="[
                'a18',
              ]"
              placeholder="请输入职务"
            />
          </a-form-item>
          <a-form-item
            label="备注信息"
            style="margin-bottom:0px;"
          >
            <a-textarea
              v-decorator="[
                'a19',
              ]"
              placeholder="请输入备注信息"
              :rows="5"
            />

          </a-form-item>
          <a-form-item
            :wrapper-col=" {
              xs: { span: 24 },
              sm: { span: 14 }
            }"
            :label-col="{
              xs: { span: 24 },
              sm: { span: 18 }
            }"
          >
            <a-row style="padding:22px;">
              <a-col :span="12"></a-col>
              <a-col :span="10">
                <a-button type="text">
                  保存为草稿
                </a-button>
                <a-button
                  style="margin-left:10px;"
                  type="primary"
                  html-type="submit"
                >
                  提交
                </a-button>
              </a-col>
            </a-row>
          </a-form-item>
        </a-form>
      </template>
    </div>

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
  name: 'RegisterAnimation',
  components: {},
  data () {
    return {
      radioCol: {
        wrapperCol: {
          xs: { span: 24 },
          sm: { span: 16 }
        },
        labelCol: {
          xs: { span: 24 },
          sm: { span: 7 }
        }
      },
      wrapperCol: {
        xs: { span: 24 },
        sm: { span: 10 }
      },
      labelCol: {
        xs: { span: 24 },
        sm: { span: 7 }
      },
      dateFormat: 'YYYY/MM/DD', // 日期格式
      previewVisible: false, // 预览model
      previewImage: '', // 预览图片地址
      fileList: [
        {
          uid: '-3',
          name: 'image.png',
          status: 'done',
          url: 'https://zos.alipayobjects.com/rmsportal/jkjgkEfvpUPVyRjUImniVslZfWPnJuuZ.png'
        }
      ],
      tagMap: [], // 特殊标签
      inputVisible: false, // 增加特殊标签显示输入框
      inputValue: '' // 特殊标签输入框内容
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
    // 表单提交
    handleSubmit (e) {
      e.preventDefault()
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values)
        }
      })
    },
    // 退出头像预览
    handleCancel () {
      this.previewVisible = false
    },
    // 头像预览
    async handlePreview (file) {
      if (!file.url && !file.preview) {
        file.preview = await getBase64(file.originFileObj)
      }
      this.previewImage = file.url || file.preview
      this.previewVisible = true
    },
    // 上传头像事件
    handleChange ({ fileList }) {
      this.fileList = fileList
    },
    // 特殊标签添加事件
    onSearch (value) {
      if (!value) return
      if (this.tagMap.indexOf(value) === -1) {
        this.tagMap.push(value)
      }
    },
    // 关闭特殊标签
    closed (i) {
      this.tagMap.splice(i, 1)
    },
    // --------------特殊标签逻辑---------------------
    handleClose (removedTag) {
      const tags = this.tagMap.filter(tag => tag !== removedTag)
      console.log(tags)
      this.tagMap = tags
    },

    showInput () {
      this.inputVisible = true
      this.$nextTick(function () {
        this.$refs.input.focus()
      })
    },

    handleInputChange (e) {
      this.inputValue = e.target.value
    },

    handleInputConfirm () {
      const inputValue = this.inputValue
      let tags = this.tagMap
      if (inputValue && tags.indexOf(inputValue) === -1) {
        tags = [...tags, inputValue]
      }
      Object.assign(this, {
        tagMap: tags,
        inputVisible: false,
        inputValue: ''
      })
      // ----------------------------
    }
  }
}
</script>
<style lang='less' scoped>
//@import url(); 引入公共css类
.registrationResidence {
  background: #fff;
  .nav-hox {
    padding: 18px 27px;
    height: 60px;
    border-bottom: 1px solid rgba(233, 233, 233, 1);
  }
  .form-hox {
    padding: 30px 0px;
    .age-hox {
      font-size: 14px;
      font-family: PingFangSC-Regular, PingFang SC;
      font-weight: 400;
      color: rgba(0, 0, 0, 0.45);
      line-height: 22px;
    }
  }
}
ant-upload-select-picture-card i {
  font-size: 32px;
  color: #999;
}

.ant-upload-select-picture-card .ant-upload-text {
  margin-top: 8px;
  color: #666;
}
.clearfix {
  display: flex;
  flex-direction: column;
}
/deep/#between {
  .ant-form-item-label {
    &::before {
      color: #f39797;
      display: inline-block;
      margin-right: 4px;
      font-size: 14px;
      font-family: SimSun, sans-serif;
      line-height: 1;
      content: '*';
    }
    label {
      color: #908e8e;
    }
  }
}
</style>
