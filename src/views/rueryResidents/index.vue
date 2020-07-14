<!--  -->
<template>
  <div class="rueryResidents">
    <div class="f-s-c">
      <h3>查询居民</h3>
      <a-button type="primary">数据导出</a-button>
    </div>
    <a-divider />
    <a-row style="margin-bottom: 24px;">
      <a-col :span="9">
        <a-input-search
          placeholder="请输入门牌号/身份证/姓名/手机号"
          enter-button="搜索"
          @search="onSearch"
        />
      </a-col>
    </a-row>
    <a-row>
      <a-col class="f-s-c">
        <h3>筛选列表</h3>
        <div @click="isRotating = !isRotating"><a>收起筛选项</a>
          <a-icon
            :class="[{'isRotating':isRotating},'rotating','m-l-10']"
            type="up"
          />
        </div>
      </a-col>
    </a-row>
    <template>
      <a-form
        layout="horizontal"
        :wrapper-col=" {
          xs: { span: 24 },
          sm: { span: 22 }
        }"
        :label-col="{
          xs: { span: 24 },
          sm: { span: 2 }
        }"
      >
        <a-form-item label="所属小区">
          <a-row>
            <template>
              <a-radio-group
                v-decorator="[
                  'radio',
                  { initialValue: 1 },
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
          <a-col :span="8">
            <a-form-item
              label="房屋"
              :wrapper-col=" {
                xs: { span: 24 },
                sm: { span: 18 }
              }"
              :label-col="{
                xs: { span: 24 },
                sm: { span: 6 }
              }"
            >
              <a-select
                v-decorator="[
                  'ac',
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
          <a-col
            :span="10"
            style="margin-left:10px;"
          >
            <a-form-item
              :wrapper-col=" {
                xs: { span: 24 },
                sm: { span: 18 }
              }"
              :label-col="{
                xs: { span: 24 },
                sm: { span: 0 }
              }"
            >
              <a-select
                v-decorator="[
                  'ad',
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
        <a-form-item label="房屋类型">
          <template>
            <a-radio-group
              v-decorator="[
                'a2',
                { initialValue: 1 },
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
                空置
              </a-radio>
            </a-radio-group>
          </template>
        </a-form-item>
        <a-form-item label="年龄">
          <a-row>
            <a-col :span="4">
              <a-input></a-input>
            </a-col>
            <a-col>
              至
            </a-col>
            <a-col :span="4">
              <a-input></a-input>
            </a-col>
          </a-row>
        </a-form-item>
        <a-form-item :wrapper-col="formItemLayout.wrapperCol">
          <a-button type="primary">
            Submit
          </a-button>
        </a-form-item>
      </a-form>
    </template>
  </div>
</template>

<script>

export default {
  components: {
  },
  data () {
    return {
      isRotating: false,
      formItemLayout: {
        labelCol: { span: 4 },
        wrapperCol: { span: 14 }
      }
    }
  },
  computed: {},
  watch: {},
  created () {

  },
  mounted () {

  },
  beforeCreate () { },
  beforeMount () { },
  beforeUpdate () { },
  updated () { },
  beforeDestroy () { },
  destroyed () { },
  activated () { },
  methods: {
    // 搜索框
    onSearch (value) {

    }
  }
}
</script>
<style lang='less' scoped>
//@import url(); 引入公共css类
.rueryResidents {
  background: #fff;
  padding: 20px 40px;
  .rotating {
    transform: rotate(0deg);
    transition: 0.5s;
  }
  .isRotating {
    transform: rotate(180deg);
    transition: 0.5s;
  }
}
</style>
