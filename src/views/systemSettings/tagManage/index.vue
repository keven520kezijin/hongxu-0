<!--  -->
<template>
  <div class="tagManage">
    <div class="f-s-c">
      <h3>标签管理</h3>
      <a-button type="primary">添加标签</a-button>
    </div>
    <a-divider />
    <a-input-search
      class="m-b-10"
      @search="onSearch"
      placeholder="请输入用户名"
      style="width: 240px"
    />
    <template>
      <a-table
        :columns="columns"
        :data-source="data"
        :loading="loading"
        :pagination="pagination"
        :row-selection="rowSelection"
        @change="handleTableChange"
      >
        <div
          class="f-s-c"
          slot="operation"
        >
          <a>删除</a>
        </div>
      </a-table>
    </template>
  </div>
</template>

<script>
const columns = [
  {
    title: '标签',
    dataIndex: 'name'
  },
  {
    title: '操作',
    dataIndex: 'operation',
    scopedSlots: { customRender: 'operation' }
  }
]
const data = [
  {
    key: '2',
    name: 'HX000000000000001',
    age: 42,
    address: 'sdd'
  },
  {
    key: '3',
    name: 'HX000000000000001',
    age: 32,
    address: '332三下乡'
  },
  {
    key: '4',
    name: 'HX000000000000001',
    age: 99,
    address: '我说的k'
  }
]
export default {
  components: {},
  data () {
    return {
      data,
      columns,
      pagination: {
        position: 'bottom',
        showQuickJumper: true
      },
      loading: false
    }
  },
  computed: {
    rowSelection () {
      return {
        onChange: (selectedRowKeys, selectedRows) => {
          console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows)
        },
        getCheckboxProps: record => ({
          props: {
            disabled: record.name === 'Disabled User', // Column configuration not to be checked
            name: record.name
          }
        })
      }
    }
  },
  watch: {},
  created () { },
  mounted () { },
  beforeCreate () { },
  beforeMount () { },
  beforeUpdate () { },
  updated () { },
  beforeDestroy () { },
  destroyed () { },
  activated () { },
  methods: {
    onSearch (value) {
      console.log(value)
    },
    handleTableChange (pagination, filters, sorter) {
      console.log(pagination)
      const pager = { ...this.pagination }
      pager.current = pagination.current
      this.pagination = pager
      /** 发送请求获取其他页数据 */
    }
  }
}
</script>
<style lang='less' scoped>
//@import url(); 引入公共css类
.tagManage {
  background: #fff;
  padding: 20px 40px;
}
</style>
