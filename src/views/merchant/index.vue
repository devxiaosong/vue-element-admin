<template>
  <div class="app-container">
    <el-select v-model="value" placeholder="请选择">
      <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label"
        :value="item.value">
      </el-option>
    </el-select>
    <span class="right-btn">
      <el-input v-model="merchantId" placeholder="搜索店铺ID" style="width: 200px;" class="filter-item" clearable/>
      <el-button type="primary" size="small" @click="handleQuery(scope)">查询</el-button>
      <el-button type="danger" size="small" align="right" @click="handleReset(scope)">重置</el-button>
    </span>

    <el-table
      :key="tableKey"
      :data="list"
      border
      fit
      highlight-current-row
      style="width: 100%;margin-top: 20px;">
      <el-table-column :label="merchant.id" min-width="60px">
        <template slot-scope="scope">
          {{ scope.row.id }}
        </template>
      </el-table-column>
      <el-table-column :label="merchant.name" min-width="60px" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.name }}</span>
        </template>
      </el-table-column>
      <el-table-column :label="merchant.balance" min-width="60px" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.balance }}</span>
        </template>
      </el-table-column>
      <el-table-column :label="merchant.todayConsumed" min-width="60px" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.todayConsumed }}</span>
        </template>
      </el-table-column>
      <el-table-column :label="merchant.average" min-width="60px" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.average }}</span>
        </template>
      </el-table-column>
      <el-table-column :label="merchant.starred" min-width="30px" align="center">
        <template slot-scope="scope">
          <el-button type="primary" size="mini" icon="el-icon-star-on" @click="handleStar(scope.row)"></el-button>
        </template>
      </el-table-column>
      <el-table-column :label="merchant.planEntry" min-width="30px" align="center">
        <template slot-scope="scope">
          <el-button type="primary" size="mini" icon="el-icon-circle-plus-outline" @click="handleAdd(scope.row)"></el-button>
        </template>
      </el-table-column>
    </el-table>

    <pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList" />

  </div>
</template>

<script>
import Pagination from '@/components/Pagination' // Secondary package based on el-pagination

export default {
  name: 'Merchant',
  components: { Pagination },
  data() {
    return {
      tableKey: 0,
      merchant: {
        id: '广告主ID',
        name: '广告主名称',
        balance: '现金余额（元）',
        todayConsumed: '今日消耗（元）',
        average: '安装均价（今天）',
        starred: '关注',
        planEntry: '新建计划'
      },
      list: [{
        id: '01',
        name: '商户01',
        balance: '1000.01',
        todayConsumed: '10.01',
        average: '1.01',
        starred: '关注',
        planEntry: '新建'
      }, {
        id: '02',
        name: '商户02',
        balance: '1000.02',
        todayConsumed: '10.02',
        average: '1.02',
        starred: '关注',
        planEntry: '新建'
      }, {
        id: '03',
        name: '商户03',
        balance: '1000.03',
        todayConsumed: '10.03',
        average: '1.03',
        starred: '关注',
        planEntry: '新建'
      }],
      options: [{
        value: '00001',
        label: '星空节点(杭州)'
      }, {
        value: '00002',
        label: '杭州爱赞'
      }, {
        value: '00003',
        label: '杭州马到'
      }],
      value: '',
      merchantId: '007',
      total: 1,
      page: 1,
      listQuery: {
        page: 1,
        limit: 30
      }
    }
  },
  methods: {
    handleQuery(scope) {

    },
    handleReset({ $index, row }) {

    },
    getList() {
    },
    handleStar(row) {
      this.$confirm('关注该商户?' + row.id, '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.$notify({
          title: '成功',
          message: '关注成功',
          type: 'success',
          duration: 2000
        })
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消'
        })
      })
    },
    handleAdd(row) {
      this.$confirm('添加推广计划?' + row.id, '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.$notify({
          title: '成功',
          message: '点击成功',
          type: 'success',
          duration: 2000
        })
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消'
        })
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  .right-btn {
    position: absolute;
    right: 10px;
  }
</style>
