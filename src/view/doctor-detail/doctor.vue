<template>
  <div class="doctor-page">
    <!-- 医生详情页面 -->
    <div class="doctor-box-top">
      <div class="top-left">
        <div class="left-avatar">
          <img src="../../assets/images/logo-min.jpg" alt="">
        </div>
        <div class="left-info">
          <div class="name">
            <span class="n">CY009</span>
            <span class="status">监测中</span>
            <span class="member">VIP1</span>
          </div>
          <div class="intro">
            <span>医生: 张晓梅</span>
            <span>年龄: 24岁</span>
            <span>职位: 二型糖尿病</span>
          </div>
          <div class="con">
            擅长：— 四年前的那个周三，凌晨两点多，距离投票站关闭仅仅数小时，大家已经知道
            了结果：特败了希拉里今选后 …
          </div>
        </div>
      </div>
      <div class="top-right">
        <div class="title">职业证书</div>
        <div class="sub_title">为患者设置控糖方案</div>
        <img src="../../assets/icons/icon-weixiu.png" alt="">
      </div>
    </div>
    <div class="doctor-box-bottom">
      <div class="tabs-top">
        <div class="tabs-item" :class="{'isActive': isActive}" @click="changeTabs">
          任务中心
        </div>
        <div class="tabs-item" :class="{'isActive': !isActive}" @click="changeTabs">
          TA的患者
        </div>
      </div>
      <div>
        <Screen></Screen>
      </div>
    </div>
  </div>
</template>

<script>
import Screen from '_c/screen'
import CountTo from '_c/count-to'
export default {
  name: 'doctor_page',
  components: {
    CountTo,
    Screen
  },
  data () {
    return {
      tabValue: '0',
      isActive: false
    }
  },
  methods: {
    changeTabs () {
      this.isActive = !this.isActive
    }
  }
}
</script>
<style lang="less" scoped>
  .size {
    width: 100%;
    height: 100%;
  }
  .doctor-box-top {
    width: 100%;
    height: 120px;
    background: #FFFFFF;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 18px 20px;
  }
  .doctor-box-bottom {
    width: 100%;
    margin-top: 20px;
    // background: #fff;
    .tabs-top {
      width: 200px;
      display: flex;
      div {
        flex: 1;
        height: 46px;
        line-height: 46px;
        text-align: center;
        border-radius: 6px 6px 0px 0px;
        background: #FFF;
        font-size: 12px;
      }
      .isActive {
        color: #9F9F9F;
        background: #EAEDF1;
      }
    }
    // height: 120px;
  }
  .top-left {
    flex: 1;
    margin-right: 200px;
    display: flex;
    .left-avatar {
      margin-right: 18px;
      img {
        width: 56px;
        height: 56px;
        border-radius: 50%;
      }
    }
    .left-info {
      .name {
        .n {
          font-size: 12px;
          font-family: PingFangSC-Medium, PingFang SC;
          font-weight: 500;
          color: #242424;
          line-height: 11px;
        }
        .status {
          display: inline-block;
          margin-left: 20px;
          margin-right: 8px;
          width: auto;
          height: 20px;
          background: #F1FCFD;
          border-radius: 3px;
          border: 1px solid #B0EDF1;
          padding: 0 3px;
          font-size: 12px;
          font-family: PingFangSC-Regular, PingFang SC;
          font-weight: 400;
          color: #00BACF;
          line-height: 18px;
        }
        .member {
          width: auto;
          height: 15px;
          background: #FFF1EB;
          border-radius: 3px;
          border: 1px solid #FFB999;
          padding: 0 3px;
          font-size: 12px;
          font-family: PingFangSC-Regular, PingFang SC;
          font-weight: 400;
          color: #FF5100;
          line-height: 14px;
        }
      }
      .intro {
        width: 70%;
        display: flex;
        justify-content: space-between;
        margin: 10px 0 12px;
        span {
          font-size: 12px;
          font-family: PingFangSC-Regular, PingFang SC;
          font-weight: 400;
          color: #242424;
          line-height: 14px;
        }
      }
      .con {
        font-size: 12px;
        font-family: PingFangSC-Regular, PingFang SC;
        font-weight: 400;
        color: #242424;
        line-height: 14px;
      }
    }
  }
  .top-right {
    width: 146px;
    height: 70px;
    background: #304ECE;
    box-shadow: 0px 1px 3px 0px rgba(235,235,235,0.5);
    border-radius: 4px;
    padding: 13px 15px;
    position: relative;
    .title {
      font-size: 14px;
      font-family: PingFangSC-Semibold, PingFang SC;
      font-weight: 600;
      color: #FFFFFF;
      line-height: 15px;
    }
    .sub_title {
      font-size: 12px;
      color: #FFFFFF;
      line-height: 15px;
      margin-top: 10px;
    }
    img {
      width: 35px;
      height: 42px;
      position: absolute;
      bottom: 10px;
      right: 10px;
    }
  }
</style>
