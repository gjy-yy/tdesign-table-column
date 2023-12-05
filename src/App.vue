<template>
  <t-card>
      <t-table
      row-key="id"
      :data="keyList"
      :loading="tableLoading"
      :columns="tableColumns"
      :pagination="pagination"
      @page-change="handlePageChange"
    >
      <template #type="{ row }">
        <t-tag v-if="row.type === 1" theme="success"> 启用中 </t-tag>
        <t-tag v-else-if="row.type === 0" theme="danger">未启用</t-tag>
        <t-tag v-else>-</t-tag>
      </template>
      <template #op="{ row }">
        <t-space>
          <t-button
            size="small"
            :theme="row.type === 1 ? 'default' : 'success'"
          
          >
            {{ row.type === 1 ? '关闭' : '启用' }}
          </t-button>
          <t-button size="small" theme="danger">删除</t-button>
        </t-space>
      </template>
    </t-table>
  </t-card>
</template>

<script setup lang="ts">
import {ref,reactive} from "vue"
// 表格列
const tableColumns = [
  {
    title: '报关行代码',
    colKey: 'agentCode',
    align: 'center',
    ellipsis: true,
    width: 200,
  },
  {
    title: '抬头名称',
    colKey: 'title',
    align: 'center',
    ellipsis: true,
    // 去除下面这行直接鬼畜
    // width: 350,
  },
  {
    title: '启用状态',
    colKey: 'type',
    align: 'center',
    ellipsis: true,
    width: 200,
  },
  {
    title: '调用次数',
    colKey: 'nums',
    align: 'center',
    ellipsis: true,
    width: 200,
  },
  {
    title: '操作',
    colKey: 'op',
    width: 100,
    align: 'center',
    fixed: 'right',
  },
];
// 表格数据
const keyList=ref([{
  id:1,
  agentCode:'123',
  title:'测试1',
  type:1,
  nums:1,
}])
// 表格loading
const tableLoading=ref(false)
// 分页数据
const pagination= reactive({
  current: 1,
  pageSize: 10,
  total: 1,
})

// 请求数据
const queryList=()=>{
  tableLoading.value=true
  setTimeout(()=>{
    tableLoading.value=false
    keyList.value=[
      {
        id:2,
        agentCode:'33029803691',
        title:'江苏里高智能家居有限公司',
        type:2,
        nums:1,
      },
      {
        id:3,
        agentCode:'12345',
        title:'测试3',
        type:3,
        nums:1,
      }
    ]
    pagination.total=1
  },100)
}

// 处理分页
const handlePageChange = (pageInfo: { current: number; pageSize: number }) => {
  pagination.current = pageInfo.current;
  pagination.pageSize = pageInfo.pageSize;
  queryList();
};
</script>

