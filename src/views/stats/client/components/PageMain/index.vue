<template>
  <div class="cs-p">
    <el-card class="box-card" shadow="never">
      <div slot="header" class="box-card-header">
        <span>今日实时</span>
        <span class="update-time">更新时间：{{updateTime}}</span>
      </div>

      <div class="cs-today flex-wrap">
        <div
          v-for="(item, key) in todayData"
          :key="key"
          class="cs-today__block">
          <div class="cs-today__content">
            <div class="cs-today__info">
              <p>{{todayMap[key]}}</p>
              <p class="cs-today__number">{{item}}</p>
            </div>
          </div>
        </div>
      </div>
    </el-card>

    <el-row :gutter="20" class="cs-mt">
      <el-col :span="14">
        <el-card class="box-card" shadow="never">
          <div slot="header" class="box-card-header">
            <span>趋势</span>
          </div>

          <ve-line
            :data="loginData"
            :colors="colors"
            :settings="chartSettings"
            :data-empty="!loginData.rows.length"/>
        </el-card>
      </el-col>

      <el-col :span="10">
        <el-card class="box-card" shadow="never">
          <div slot="header" class="box-card-header">
            <span>会员等级</span>
          </div>

          <ve-pie
            :data="levelData"
            :colors="colors"
            :data-empty="!levelData.rows.length"/>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import colors from '@/plugin/careyshop/charts'
import 'v-charts/lib/style.css'

export default {
  components: {
    VeLine: () => import('v-charts/lib/line.common'),
    VePie: () => import('v-charts/lib/pie.common')
  },
  props: {
    todayData: {
      default: () => {}
    },
    levelData: {
      default: () => {}
    },
    loginData: {
      default: () => {}
    },
    updateTime: {
      default: ''
    }
  },
  data() {
    return {
      colors,
      todayMap: {
        count: '客户合计',
        enable: '正常会员',
        disable: '停用会员',
        new: '今日新增',
        active: '活跃会员'
      },
      chartSettings: {
        labelMap: {
          count: '注册量'
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.update-time {
  font-size: 12px;
  color: $color-info;
  float: right;
}

.box-card {
  border-radius: 0;
  border: 1px solid $color-border-1;
}

.box-card-header {
  font-size: 14px;
  color: $color-text-normal;
}

.flex-wrap {
  display: flex;
  flex-wrap: wrap;
  margin: -10px;
}

.cs-today {
  .cs-today__block {
    width: 20%;
    box-sizing: border-box;
  }

  .cs-today__content {
    display: flex;
    color: $color-info;
    border-radius: 4px;
    background-color: #F5F7FA;
    margin: 10px;
    overflow: hidden;
  }

  .cs-today__info {
    width: 100%;
    text-align: center;

    p {
      margin: 10px;
      font-size: 14px;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .cs-today__number {
      color: $color-text-normal;
      font-size: 28px;
    }
  }
}
</style>
