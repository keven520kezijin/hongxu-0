<!--  -->
<template>
  <div class="memberMange">
    <div class="f-s-c">
      <h3>成员管理</h3>
      <a-button type="primary">添加成员</a-button>
    </div>
    <a-divider />
    <a-input-search
      class="m-b-10"
      @search="onSearch"
      placeholder="请输入用户名"
      style="width: 240px"
    />
    <template>
      <div class="table-wrap">
        <a-table
          :rowKey="record => record.id"
          :columns="columns"
          :data-source="data"
          :loading="loading"
          :pagination="pagination"
          @change="handleTableChange"
          :row-selection="{ selectedRowKeys: selectedRowKeys, onSelect: onSelectChange, onSelectAll: onSelectAll }"
        >
          <!-- <span slot="selectAll">
            <a-checkbox @change="onSelectedAll">
            </a-checkbox>
          </span>
          <span
            slot="select"
            slot-scope="recordId"
          >
            <a-checkbox
              @change="(e)=>onSelected(e,recordId)"
              v-model="checked"
            >
            </a-checkbox>
          </span> -->
          <div
            class="f-s-c"
            slot="operation"
          >
            <a>查看/编辑</a>
            <a>重置密码</a>
            <a>删除</a>
          </div>
        </a-table>
        <div class="deleteAll f-s-c">
          <a-checkbox @change="onSelectedAll">
          </a-checkbox>
          <a-button type="primary">删除</a-button>
        </div>
      </div>

    </template>
  </div>
</template>

<script>
const columns = [
  // {
  //   dataIndex: 'id',
  //   scopedSlots: {
  //     title: 'selectAll',
  //     customRender: 'select'
  //   }
  // },
  {
    title: '编号',
    dataIndex: 'name'
  },
  {
    title: '用户名',
    dataIndex: 'age'
  },
  {
    title: '手机号',
    dataIndex: 'address'
  },
  {
    title: '职务',
    dataIndex: 'a'
  },
  {
    title: '初始密码',
    dataIndex: 'b'
  },
  {
    title: '操作',
    dataIndex: 'operation',
    scopedSlots: { customRender: 'operation' }
  }
]
const data = [
]
for (let i = 0; i < 22; i++) {
  data.push({
    id: 'a12344' + i,
    key: '1',
    name: 'HX000000000000001',
    age: 32,
    address: '1234---',
    a: '123',
    b: '234'
  })
}
export default {
  name: 'MemberMange',
  components: {},
  data () {
    return {
      data,
      columns,
      // 分页
      pagination: {
        position: 'bottom',
        showQuickJumper: true
      },
      loading: false,
      selectedRowKeys: [], // 所有被选中的列id
      isSelectedAll: false // 是否选中所有
    }
  },
  computed: {
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
      /** 如果全选，翻页后把请求返回的数据的id过滤后存入selectedRowKeys中 */
      if (this.isSelectedAll) {
        const ids = Array.from(new Set(data.map(v => v.id).concat(this.selectedRowKeys)))
        this.selectedRowKeys = ids
      }
    },
    // 删除的选中所有
    onSelectedAll (e) {
      console.log('checkedValue', e)
    },
    // 多选框值改变
    onSelectChange (record, selected, selectedRows, nativeEvent) {
      console.log('selectedRowKeys changed: ', record, selected, selectedRows, nativeEvent)
      if (selected) {
        this.selectedRowKeys.push(record.id)
      } else {
        this.selectedRowKeys = this.selectedRowKeys.filter(v => v !== record.id)
      }
    },
    onSelectAll (selected, selectedRows, changeRows) {
      if (selected) {
        this.isSelectedAll = true
        this.selectedRowKeys.push(...selectedRows.map(v => v.id))
      } else {
        this.isSelectedAll = false
        this.selectedRowKeys = []
      }
      console.log('selected, selectedRows, changeRows------', selected, selectedRows, changeRows)
    }
  }
}
</script>
<style lang='less' scoped>
//@import url(); 引入公共css类
.memberMange {
  background: #fff;
  padding: 20px 40px;
  .table-wrap {
    position: relative;
    .deleteAll {
      position: absolute;
      width: 100px;
      bottom: 20px;
      left: 20px;
    }
  }
}
</style>
