<template>
  <div class="app-container">
    <el-form v-if="form.id" ref="form" :inline="true" :model="form" :rules="rules" class="demo-form-inline">
    <el-row :gutter="10">
      <el-col :span="24">
        <div class="grid-content bg-purple">
          <span align="center">计划设置</span>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :span="12">
        <div class="grid-content bg-purple">
        定向设置
          <el-row>所选定向：家居30（35-55）</el-row>
          <el-container style="height: 200px; border: 1px solid #eee">
            <el-main>
            <el-row>性别：男</el-row>
            <el-row>年龄：35至55岁</el-row>
            <el-row>联网方式：Wifi，3G，4G</el-row>
            <el-row>地理位置：上海市，上海市，上海市，上海市，上海市，上海市，上海市，上海市，上海市，上海市，上海市，上海市上海市，上海市，上海市，上海市，上海市，上海市上海市，上海市，上海市，上海市，上海市，上海市上海市，上海市，上海市，上海市，上海市，上海市</el-row>
            <el-row>行为兴趣：场景</el-row>
            </el-main>
          </el-container>
        </div>
      </el-col>
      <el-col :span="4">
        <div class="grid-content bg-purple">
        定向名称
          <el-container style="height: 200px; border: 1px solid #eee">
            <el-main>
              <el-table
                :show-header="showHeader"
                ref="singleTable"
                :data="tableData"
                highlight-current-row
                style="width: 100%">
                <el-table-column
                  property="date"
                  label="定向包名"
                  width="120">
                </el-table-column>
              </el-table>
            </el-main>
          </el-container>
        </div>
      </el-col>
      <el-col :span="8">
        <div class="grid-content bg-purple">
        资源位设置
          <el-container style="height: 200px; border: 1px solid #eee">
            <el-main>
              <el-table
                ref="singleTable"
                :data="resourceData"
                highlight-current-row
                style="width: 100%">
                <el-table-column
                  property="position"
                  label="广告版位"
                  width="60">
                </el-table-column>
                <el-table-column
                  property="size"
                  label="尺寸"
                  width="60">
                </el-table-column>
                <el-table-column
                  property="material"
                  label="创意形式"
                  width="60">
                </el-table-column>
                <el-table-column
                  property="note"
                  label="描述"
                  width="60">
                </el-table-column>
                <el-table-column
                  property="exposure"
                  label="曝光量"
                  width="60">
                </el-table-column>
                <el-table-column
                  property="selected"
                  label="当前选择"
                  width="60">
                </el-table-column>
              </el-table>
            </el-main>
          </el-container>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :span="24">
        <div class="grid-content bg-purple">
          <el-row>创意设置</el-row>
          <el-row>请选择1张582*166分辨率的图片：</el-row>
          <el-row>暂无数据~</el-row>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="10">
      <el-col :span="24">
        <div class="grid-content bg-purple">
          <el-row>排期于出价设置</el-row>
          <el-row>
            <el-form-item label="投放日期:" prop="positionName">
              <el-radio v-model="form.positionName" label="1">长期投放</el-radio>
              <el-radio v-model="form.positionName" label="2">在日期范围内投放</el-radio>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="开始日期:" prop="positionName">
              <el-date-picker
                v-model="dateValue"
                type="date"
                placeholder="选择日期">
              </el-date-picker>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="投放方式:" prop="positionName">
              <el-radio v-model="form.positionName" label="1">CPC</el-radio>
              <el-radio v-model="form.positionName" label="2">CPM</el-radio>
              <el-radio v-model="form.positionName" label="3">oCPA</el-radio>
            </el-form-item>
          </el-row>
          <el-row>
            <el-form-item label="投放额度" prop="positionName">
              <el-input value="11" width="5px" />元/点击
            </el-form-item>
          </el-row>
          <el-row>
            <el-button type="info" plain size="medium">取消</el-button>
            <el-button type="primary" size="medium">确定</el-button>
          </el-row>
        </div>
      </el-col>
    </el-row>
    </el-form>
  </div>
</template>

<script>

export default {
  name: 'AddPlan',
  components: { },
  data() {
    return {
      showHeader: false,
      tableData: [{
        date: '家装40+'
      }, {
        date: '家装45+'
      }, {
        date: '家装50+'
      }, {
        date: '家装0+'
      }],
      resourceData: [{
        position: '移动原生',
        size: '1280x720',
        material: '多图(文)',
        note: '原生广告位',
        exposure: '0',
        selected: true
      }, {
        position: '微信',
        size: '960x334',
        material: '单图(文)',
        note: '小程序',
        exposure: '0',
        selected: false
      }, {
        position: '微信',
        size: '960x540',
        material: '单图(文)',
        note: '公众号文中广告',
        exposure: '0',
        selected: false
      }, {
        position: 'QQ空间、QQ、浏览器',
        size: '1000x560',
        material: '单图(文)',
        note: 'QQ空间、看点、动漫及浏览器等优质广告位',
        exposure: '0',
        selected: false
      }],
      dateValue: '',
      form: {
        id: 1
      },
      rules: {
      }
    }
  },
  methods: {

  }
}
</script>

<style>
  .el-row {
    margin-bottom: 20px;
  &:last-child {
     margin-bottom: 0;
   }
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
</style>
