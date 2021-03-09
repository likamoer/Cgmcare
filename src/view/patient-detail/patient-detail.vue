<template>
  <div class="doctor-page">
    <!-- 患者详情页面 -->
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
            <span class="name">
              姓名:
              <span v-show="nameFlag">张晓梅</span>
              <input ref="nameInput" v-show='!nameFlag' v-model="nameValue" @keyup.enter="complateEditor" @blur="complateEditor"  style="width: 100px" />
              <Icon type="md-checkbox-outline" v-show="nameFlag" @click="changeNameFlag" />
            </span>
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
        <div class="fangan">
          <div class="title">控糖方案</div>
          <div class="sub_title">为患者设置控糖方案</div>
          <img src="../../assets/icons/icon-weixiu.png" alt="">
        </div>
        <div class="dangan">
          <div class="title">健康档案</div>
          <div class="sub_title">患者的详细健康数据</div>
          <img src="../../assets/icons/icon-dangan.png" alt="">
        </div>
      </div>
    </div>
    <div class="doctor-box-bottom">
      <div class="tabs-top">
        <div class="tabs-item" v-for="(item, index) in tabsData" :key="index" :class="{'isActive': item.isActive}" @click="changeTabs(item)">
          {{item.name}}
        </div>
      </div>
      <div class="tabs-content">

        <Xuetang></Xuetang>
      </div>
    </div>
  </div>
</template>

<script>
import Screen from '_c/screen'
import Xuetang from './components/xuetang'
import CountTo from '_c/count-to'
export default {
  name: 'patient-detail',
  components: {
    CountTo,
    Screen,
    Xuetang
  },
  data () {
    return {
      tabsData: [
        { name: '血糖监测', value: 0, isActive: true },
        { name: '每日数据', value: 1, isActive: false },
        { name: '数据统计', value: 2, isActive: false },
        { name: '历史周期', value: 3, isActive: false }
      ],
      nameValue: '',
      nameFlag: true,
      tabValue: '0',
      isActive: false
    }
  },
  methods: {
    changeTabs (data) {
      this.tabsData.forEach((item) => {
        item.isActive = false
      })
      data.isActive = true
    },
    changeNameFlag () {
      console.log(this.$refs)
      this.nameFlag = false
      this.$refs.nameInput.focus()
    },
    complateEditor () {
      console.log(this.nameValue, '===')
      this.nameFlag = true
      this.nameValue = ''
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
      width: 400px;
      display: flex;
      div {
        flex: 1;
        height: 46px;
        line-height: 46px;
        text-align: center;
        border-radius: 6px 6px 0px 0px;
        background: #EAEDF1;
        color: #9F9F9F;
        font-size: 12px;
        margin-right: 2px;
      }
      .isActive {
        color: #333;
        background: #fff;
      }
    }
    .tabs-content {
      width: 100%;
      background: #fff;
      padding: 20px 30px;
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
        .name {
          input {
            border: 0px;
            outline: none;
            border-bottom: 1px solid #ccc;
          }
          i {
            font-size: 14px;
            display: inline-block;
            margin-left: 10px;
            color: #00BACF;
          }
        }
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
    width: 320px;
    height: 70px;
    display: flex;
    .fangan {
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
    .dangan {
      background: #16CCA6;
      box-shadow: 0px 1px 3px 0px rgba(235,235,235,0.5);
      border-radius: 4px;
      padding: 13px 15px;
      position: relative;
      margin-left: 10px;
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
        width: 45px;
        height: 42px;
        position: absolute;
        bottom: 10px;
        right: 10px;
      }
    }
  }
</style>
