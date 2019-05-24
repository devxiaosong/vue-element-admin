<template>
  <div class="app-container">
    <el-form v-if="form.id" ref="form" :inline="true" :model="form" :rules="rules" class="demo-form-inline">
      <el-row>
        <el-form-item label="推广目标:">
          <span>电商网页</span>
        </el-form-item>
        <el-form-item label="日限额度(元):" prop="phoneMob">
          <el-input v-model="form.phoneMob"/>
        </el-form-item>
        <el-form-item label="投放模式:" prop="unitName">
          <el-switch
            v-model="form.unitName"
            active-text="标准投放"
            inactive-text="加速投放">
          </el-switch>
        </el-form-item>
      </el-row>
      <el-row>
        <el-form-item label="落地页面:" prop="positionName">
          <el-radio v-model="form.positionName" label="1">单品页</el-radio>
          <el-radio v-model="form.positionName" label="2">集合页</el-radio>
        </el-form-item>
      </el-row>
      <el-row>
        <el-form-item label="">
          <el-select v-model="singleGoodsValue" placeholder="请选择单品页">
            <el-option
              v-for="item in singleGoodsOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="">
          <el-select v-model="togetherGoodsValue" placeholder="请选择集合页">
            <el-option
              v-for="item in togetherGoodsOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>
      </el-row>
    </el-form>
    <el-button type="primary" size="small" @click="handleCopy(scope)">复制计划</el-button>
    <el-button type="primary" size="small" @click="handleBatchCopy(scope)">批量复制计划</el-button>

    <el-table
      :key="tableKey"
      :data="list"
      border
      fit
      highlight-current-row
      style="width: 100%;margin-top: 20px;">
      <el-table-column :label="merchant.id" min-width="15px" align="center">
        <template slot-scope="scope">
          {{ scope.$index + 1 }}
        </template>
      </el-table-column>
      <el-table-column :label="merchant.filterParam" min-width="60px" align="center">
        <template slot-scope="scope">
          <el-select v-model="scope.row.filterParam" placeholder="请选择">
            <el-option
              v-for="item in filterOption"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </template>
      </el-table-column>
      <el-table-column :label="merchant.location" min-width="30px" align="center">
        <template slot-scope="scope">
          <span>{{ scope.row.location }}</span>
        </template>
      </el-table-column>
      <el-table-column :label="merchant.material" min-width="60px" align="center">
        <template slot-scope="scope">
          <img :src="url" class="user-avatar">
        </template>
      </el-table-column>
      <el-table-column :label="merchant.plan" min-width="60px" align="center">
        <template slot-scope="scope">
          <el-row>
            <span>长期投放，2019-05-22开始</span>
          </el-row>
          <el-row>
            <span>全天投放 oCPA</span>
          </el-row>
          <el-row>
            <el-input value="11" width="10px" />元
          </el-row>
        </template>
      </el-table-column>
      <el-table-column :label="merchant.action" min-width="30px" align="center">
        <template slot-scope="scope">
          <el-row>
            <div class="grid-content">
              <el-button type="primary" size="mini" icon="el-icon-edit" @click="handleEdit(scope.row)">编辑</el-button>
            </div>
          </el-row>
          <el-row>
            <div class="grid-content">
              <el-button type="danger" size="mini" icon="el-icon-delete" @click="handleDelete(scope.row)">删除</el-button>
            </div>
          </el-row>
        </template>
      </el-table-column>
    </el-table>

    <el-button type="success" size="small" align="middle" icon="el-icon-edit" @click="handleCreate(scope)">设置计划</el-button>

  </div>
</template>

<script>

export default {
  name: 'Merchant',
  components: { },
  data() {
    return {
      url: 'https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
      fit: 'scale-down',
      form: {
        operatorRealName: '',
        phoneMob: '',
        unitName: '',
        positionName: '',
        id: 1
      },
      rules: {
        operatorRealName: [
          { required: true, message: '请填写姓名', trigger: 'blur' },
          { min: 1, max: 5, message: '姓名长度在 1 到 5 个字符', trigger: 'blur' }
        ],
        phoneMob: [
          { required: true, message: '请填写手机', trigger: 'blur' },
          { min: 1, max: 5, message: '姓名长度在 1 到 5 个字符', trigger: 'blur' }
        ],
        unitName: [
          { required: true, message: '请填写单位', trigger: 'blur' },
          { min: 1, max: 20, message: '单位长度在 1 到 20 个字符', trigger: 'blur' }
        ],
        positionName: [
          { min: 1, max: 20, message: '岗位长度在 1 到 20 个字符', trigger: 'blur' }
        ]
      },
      tableKey: 0,
      filterOption: [{
        value: '00001',
        label: '通40+'
      }, {
        value: '00002',
        label: '通60+'
      }, {
        value: '00003',
        label: '通45+'
      }],
      merchant: {
        id: '序号',
        filterParam: '定向包',
        location: '资源位',
        material: '创意',
        plan: '排期与出价',
        action: '操作'
      },
      list: [{
        id: '01',
        filterParam: '00001',
        location: '微信',
        material: '广告创意',
        plan: '投放计划',
        action: '新建'
      }, {
        id: '02',
        filterParam: '00002',
        location: '微信',
        material: '广告创意',
        plan: '投放计划',
        action: '新建'
      }, {
        id: '03',
        filterParam: '00003',
        location: '微信',
        material: '广告创意',
        plan: '投放计划',
        action: '新建'
      }],
      singleGoodsOptions: [{
        value: '00001',
        label: '电热水器'
      }, {
        value: '00002',
        label: '冷风机'
      }, {
        value: '00003',
        label: '少儿成长书6本'
      }],
      togetherGoodsOptions: [{
        value: '00001',
        label: '古驰鞋'
      }, {
        value: '00002',
        label: '爱赞衣服'
      }, {
        value: '00003',
        label: '马到手表'
      }],
      singleGoodsValue: '',
      togetherGoodsValue: '',
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
    handleCopy(row) {
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
    handleEdit(row) {
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
    handleDelete(row) {
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
    handleCreate(row) {
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
    handleBatchCopy(row) {
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

  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }

  .user-avatar {
    cursor: pointer;
    width: 40px;
    height: 40px;
  }
</style>
