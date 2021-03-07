<template>
  <div class="monitor-page">
    <!-- 监控中心页面 -->
    <!-- 顶部 -->
    <div class="monitor-top">
      <info-card class="top-card" shadow :color="'#ccc'" :title='"我的患者"' :icon-size="22" @add="add" @go='go'>
        <div class="content">
          <div class="patient-now" v-for="(item, index) in 3" :key="index">
            <div class="title">佩戴用户</div>
            <div class="num"><count-to :end="2020" count-class="count-style"/></div>
          </div>
        </div>
      </info-card>
      <info-card class="top-card" shadow :color="'#ccc'" :title='"我的任务"' :icon-size="22" @add="add" @go='go'>
        <div class="content-middle">
          <div class="report">
            <Badge :count="1000" overflow-count="999">
              <a href="#" class="demo-badge"></a>
            </Badge>
            <div class="img">
              <img src="../../assets/icons/report.png" alt="">
            </div>
            <div class="title">
              报告解读
            </div>
          </div>
          <div class="plan">
            <Badge :count="1000" overflow-count="999">
              <a href="#" class="demo-badge"></a>
            </Badge>
            <div class="img">
              <img src="../../assets/icons/plan.png" alt="">
            </div>
            <div class="title">
              食药计划
            </div>
          </div>
        </div>
      </info-card>
      <info-card class="top-card" shadow :color="'#ccc'" :title='"我的团队"' :icon-size="22" @add="add" @go='go'>
        <div class="content-bottom">
          <div class="avatars" v-for="(item, index) in 4" :key="index">
            <div class="img">
              <img src="../../assets/images/logo.jpg" alt="">
            </div>
            <div class="title">
              张一元
            </div>
            <div class="tag">
              医生
            </div>
          </div>
        </div>
      </info-card>
    </div>
    <!-- 中部 -->
    <div class="monitor-middle">
      <div class="for-data-list" v-for="(itx, idx) in 3" :key='idx'>
        <info-card class="top-card" shadow :addShow='false' :color="'#ccc'" :title='"高血糖事件"' :icon-size="22" @add="add" @go='go'>
          <div class="content">
            <div class="item-list" v-for="(item, index) in 4" :key='index'>
              <div class="name">年底万达网</div>
              <div class="time">12:33</div>
              <div class="change">高血糖预警: 11.4mmol/L</div>
            </div>
          </div>
        </info-card>
      </div>
    </div>
    <!-- 底部 -->
    <div class="monitor-bottom">
      <info-card class="top-card" shadow :addShow='false' :goShow='false' :isLine='false' :color="'#ccc'" :title='"年龄统计"' :icon-size="22" @add="add" @go='go'>
        <div class="content">
          <chart-bar style="height: 300px;" :value="barData" text="年龄,性别,患病类型"/>
        </div>
      </info-card>
      <info-card class="top-card" shadow :addShow='false' :goShow='false' :isLine='false' :color="'#ccc'" :title='"类型统计"' :icon-size="22" @add="add" @go='go'>
        <div class="content">
          <chart-pie style="height: 300px;" :value="pieData" text="性别比例"></chart-pie>
          <chart-pie style="height: 300px;" :value="pieData" text="患病类型"></chart-pie>
        </div>
      </info-card>
    </div>
  </div>
</template>

<script>
import InfoCard from '_c/info-card'
import CountTo from '_c/count-to'
import { ChartPie, ChartBar } from '_c/charts'
export default {
  name: 'index_page',
  components: {
    InfoCard,
    CountTo,
    ChartPie,
    ChartBar
  },
  data () {
    return {
      pieData: [
        { value: 335, name: '直接访问' },
        { value: 310, name: '邮件营销' },
        { value: 234, name: '联盟广告' },
        { value: 135, name: '视频广告' },
        { value: 1548, name: '搜索引擎' }
      ],
      barData: {
        '1-10': 13253,
        '10-20': 34235,
        '20-30': 26321,
        '30-40': 12340,
        '40-50': 24643,
        '50-60': 1322,
        '60-70': 1324
      }
    }
  },
  methods: {
    add () {
      console.log('11')
    },
    go () {
      console.log('111111')
    }
  }
}
</script>
<style lang="less">
  .size {
    width: 100%;
    height: 100%;
  }
  .monitor-top {
    display: flex;
    .top-card {
      flex: 1;
      margin-right: 20px;
    }
    .top-card:last-child {
      margin-right: 0px;
    }
     .content {
    width: 100%;
    padding: 0 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 60px;
    .patient-now {
      width: 100%;
      .title {
        font-size: 12px;
        font-family: PingFangSC-Regular, PingFang SC;
        font-weight: 400;
        color: #242424;
        line-height: 10px;
        margin-bottom: 5px;
        text-align: center;
      }
      .num {
        font-size: 20px;
        font-family: PingFangSC-Medium, PingFang SC;
        font-weight: 500;
        color: #242424;
        line-height: 28px;
        text-align: center;
      }
    }
  }
  .content-middle {
    width: 100%;
    padding: 7px 20px 0;
    display: flex;
    height: 60px;
    justify-content: space-evenly;
    align-items: center;
    .img {
      width: 33px;
      height: 33px;
    }
    img {
      width: 33px;
      height: 33px;
    }
    .title {
      font-size: 12px;
      font-family: PingFangSC-Regular, PingFang SC;
      font-weight: 400;
      color: #9F9F9F;
      line-height: 10px;
      margin-top: 2px;
    }
    .report,
    .plan {
      position: relative;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
    .ivu-badge {
      position: absolute;
      right: 0;
      top: 10px;
    }
  }
  .content-bottom {
    height: 60px;
    width: 100%;
    display: flex;
    justify-content: space-between;
    .avatars {
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
    .img {
      width: 25px;
      height: 25px;
      img {
        width: 100%;
        height: 100%;
        border-radius: 50%;
      }
    }
    .title {
      font-size: 14px;
      font-family: PingFangSC-Medium, PingFang SC;
      font-weight: 500;
      color: #242424;
      line-height: 14px;
      margin: 3px 0;
    }
    .tag {
      font-size: 12px;
      font-family: PingFangSC-Medium, PingFang SC;
      font-weight: 500;
      color: #979797;
      line-height: 12px;
    }
  }
  }
  .monitor-middle {
    display: flex;
    margin-top: 20px;
    .for-data-list {
      flex: 1;
      margin-right: 20px;
    }
    .for-data-list:last-child {
      margin-right: 0px;
    }
    .content {
    }
    .item-list {
      display: flex;
      justify-content: space-between;
      padding: 0 5px;
      margin-bottom: 14px;
      .name {
        font-size: 12px;
        font-family: PingFangSC-Regular, PingFang SC;
        font-weight: 400;
        color: #242424;
        line-height: 14px;
      }
    }
  }
  .monitor-bottom {
    display: flex;
    margin-top: 20px;
    .top-card {
      flex: 1;
      margin-right: 20px;
      // overflow: hidden;
    }
    .top-card:last-child {
      margin-right: 0px;
    }
    .content {
      .size;
      width: 90%;
      margin: 0 auto;
      height: 300px;
      display: flex;
      .charts {
        .size;
      }
    }
  }
  .join-page{
    text-align: center;
  }
  .qq-group-img{
    width: 100%;
  }
  .join-page-other-icon{
    width: 20px;
    vertical-align: middle;
    margin-right: 6px;
  }
  .join-page-other{
    text-align: left;
  }
  .join-page-other .ivu-btn{
    margin-right: 6px;
  }
</style>
