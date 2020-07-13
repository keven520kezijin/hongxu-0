<!--  -->
<template>
  <div class="accessLog">
    <div class="f-s-c">
      <h3>访问日志</h3>
      <div></div>
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
      </a-table>
    </template>
  </div>
</template>

<script>
const columns = [
  {
    title: '编号',
    dataIndex: 'name'
  },
  {
    title: '用户名',
    dataIndex: 'a'
  },
  {
    title: '手机号',
    dataIndex: 'b'
  },
  {
    title: '职务',
    dataIndex: 'c'
  },
  {
    title: '访问时间',
    dataIndex: 'd'
  }
]
const data = [
  {
    a: '2',
    name: 'HX000000000000001',
    b: 42,
    c: 'sdd',
    d: 'sdd'
  },
  {
    a: '2',
    name: 'HX000000000000001',
    b: 42,
    c: 'sdd',
    d: 'sdd'
  },
  {
    a: '2',
    name: 'HX000000000000001',
    b: 42,
    c: 'sdd',
    d: 'sdd'
  },
  {
    a: '2',
    name: 'HX000000000000001',
    b: 42,
    c: 'sdd',
    d: 'sdd'
  },
  {
    a: '2',
    name: 'HX000000000000001',
    b: 42,
    c: 'sdd',
    d: 'sdd'
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
.accessLog {
  background: #fff;
  padding: 20px 40px;
}
</style>
