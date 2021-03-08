<template>
  <Modal
    v-model="visible"
    :title="title"
    @on-ok="ok"
    @on-cancel="cancel"
    okText="确定"
    cancelText="清空"
    width="1240"
  >
    <div class="main">
      <div class="addPlanArea">
        <div class="formBox">
          <Form :model="activityForm" label-position="left" :label-width="72">
            <FormItem class="formItem" label="方案名称：">
              <Input class="formInput" v-model="activityForm.name" placeholder="输入方案名称" />
              <div class="choosePlan">选择方案模板</div>
            </FormItem>
            <FormItem class="formItem" label="开始日期：">
              <DatePicker
                class="formInput"
                v-model="activityForm.date"
                type="date"
                placeholder="选择开始日期"
              ></DatePicker>
            </FormItem>
            <FormItem class="formItem" label="执行天数：">
              <Select class="formInput" v-model="activityForm.time" placeholder="选择执行天数">
                <Option v-for="item in [3,7]" :value="item" :key="item">{{ item }}天</Option>
              </Select>
            </FormItem>
            <div class="worker">
              <FormItem class="formItem" label="负 责 人 ：">
                <div class="workerList">
                  <div class="workerItem">
                    <img
                      src
                      onerror="this.src='https://webimg.ziroom.com/1c853bc6-21fc-4e32-8a6f-18ec2c6fef32.png'"
                    />
                    <p class="name">张一元</p>
                  </div>
                </div>
              </FormItem>
              <FormItem class="formItem" style="margin-left:44px;" label="参与人员：">
                <div class="workerList">
                  <div class="workerItem">
                    <img
                      src
                      onerror="this.src='https://webimg.ziroom.com/1c853bc6-21fc-4e32-8a6f-18ec2c6fef32.png'"
                    />
                    <p class="name">张一元</p>
                  </div>
                  <div class="workerItem">
                    <img
                      src
                      onerror="this.src='https://webimg.ziroom.com/1c853bc6-21fc-4e32-8a6f-18ec2c6fef32.png'"
                    />
                    <p class="name">张一元</p>
                  </div>
                </div>
              </FormItem>
            </div>
          </Form>

          <div class="dateList">
            <div
              class="dateItem"
              :class="[index==0?'active':'']"
              v-for="(item,index) in 7"
              :key="index"
            >
              <div class="date">12</div>
              <div class="week">星期一</div>
            </div>
          </div>

          <div class="energyList">
            <div class="total">
              <span class="bold">总热量：</span>
              <span class="light">251231</span>
              <span class="grey">千卡</span>
            </div>
            <div class="subItem">
              <span class="grey">碳水</span>
              <img class="icon" src="../../assets/icons/tanshui.png" />
              <span class="count">1200克</span>
            </div>
            <div class="subItem">
              <span class="grey">蛋白质</span>
              <img class="icon" src="../../assets/icons/danbai.png" />
              <span class="count">120克</span>
            </div>
            <div class="subItem">
              <span class="grey">脂肪</span>
              <img class="icon" src="../../assets/icons/zhifang.png" />
              <span class="count">140克</span>
            </div>
          </div>
        </div>
      </div>
      <div class="line"></div>
      <div class="previewArea">
        <div class="header">
          <div class="title">方案预览</div>
          <div class="dots">
            <div class="item">
              <p class="dot" style="background: #242424;"></p>食物
            </div>
            <div class="item">
              <p class="dot" style="background: #16CCA6;"></p>药物
            </div>
            <div class="item">
              <p class="dot" style="background: #32C5FF;"></p>运动
            </div>
          </div>
        </div>
        <div class="tableBox">
          <div class="theader">
            <div style="width:60px"></div>
            <div class="cols">
              <div class="col">早餐</div>
              <div class="col">午餐</div>
              <div class="col">晚餐</div>
              <div class="col">加餐</div>
            </div>
          </div>
          <div class="tbody">
            <div class="row">
              <div class="date">1<br><br><br></div>
              <div class="rowItem"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </Modal>
</template>
<script>
export default {
  name: 'addActivityModel',
  props: {
    activityData: { type: Object },
    show: Boolean,
    title: String
  },
  data () {
    return {
      visible: this.show,
      activityForm: {
        name: '',
        date: '',
        time: ''
      }
    }
  },
  watch: {
    show (newv, oldv) {
      this.visible = newv
    }
  },
  mounted () {},
  methods: {
    ok () {
      this.visible = false
      if (this.isEdited) this.$emit('mdyData', this.data)
      this.$emit('showModel', this.visible)
    },
    cancel () {
      this.visible = false
      this.$emit('showModel', this.visible)
    }
  }
}
</script>
<style lang="less" scoped>
.main {
  box-sizing: border-box;
  width: 100%;
  height: 60vh;
  overflow-y: scroll;
  display: flex;
  justify-content: space-between;
  .line {
    width: 1px;
    height: 100%;
    background: #f4f4f4;
  }
  .addPlanArea {
    width: 600px;
    padding: 10px 40px;
    box-sizing: border-box;
    .formItem {
      height: 28px;
      margin-bottom: 12px;
      .choosePlan {
        width: 98px;
        height: 32px;
        background: #f0f2f5;
        border-radius: 3px;
        border: 1px solid #d7dbe0;
        border-radius: 3px;
        font-size: 12px;
        color: #242424;
        text-align: center;
        line-height: 30px;
        display: inline-block;
        margin-left: 12px;
      }
      .formInput {
        width: 188px;
      }
    }
    .worker {
      margin: 18px 0 0;
      padding-bottom: 8px;
      display: flex;
      border-bottom: 1px solid #f4f4f4;
      .formItem {
        height: auto;
        margin-bottom: 0;
      }
      .workerList {
        display: flex;
      }
      .workerItem {
        justify-content: center;
        align-items: flex-start;
        display: flex;
        width: 35px;
        flex-wrap: wrap;
        margin-right: 23px;
        img {
          width: 35px;
          height: 35px;
          border-radius: 50%;
          background-color: #fefefe;
          flex-shrink: 0;
        }
        .name {
          height: 18px;
          font-size: 12px;
          color: #9f9f9f;
          line-height: 18px;
          white-space: nowrap;
        }
      }
      .workerItem:last-child {
        margin-right: 0;
      }
    }
    .dateList {
      transition: all 0.3s;
      padding: 12px 0 18px;
      display: flex;
      flex-wrap: nowrap;
      width: 100%;
      overflow-x: scroll;
      .dateItem {
        width: 64px;
        height: 64px;
        background: #ffffff;
        border-radius: 4px;
        border: 1px solid #cecece;
        margin-right: 12px;
        position: relative;
        .date {
          font-size: 12px;
          color: #aaaaaa;
          position: absolute;
          left: 15px;
          top: 10px;
        }
        .week {
          text-align: center;
          margin-top: 36px;
          font-size: 13px;
          font-family: PingFangSC-Semibold, PingFang SC;
          font-weight: 600;
          color: #242424;
        }
      }
      .dateItem.active {
        background: #13be9b;
        border: 0 none;
        .date {
          color: #fff;
        }
        .week {
          color: #fff;
        }
      }
      .dateItem.active::after {
        display: block;
        content: "";
        border-width: 8px 8px 8px 8px;
        border-style: solid;
        border-color: #13be9b transparent transparent transparent;
        position: absolute;
        left: 50%;
        transform: translateX(-50%);
        top: 100%;
      }
      .dateItem:last-child {
        margin-right: 0;
      }
    }
    .energyList {
      height: 54px;
      background: #fafafa;
      display: flex;
      align-items: center;
      padding-left: 11px;
      .total {
        display: flex;
        align-items: center;
        margin-right: 38px;
      }
      .subItem {
        display: flex;
        align-items: center;
        margin-right: 25px;
      }
      .subItem:last-child {
        margin-right: 0;
      }
      .bold {
        font-family: PingFangSC-Medium, PingFang SC;
        font-weight: 500;
        color: #242424;
      }
      .light {
        font-size: 18px;
        font-family: PingFangSC-Medium, PingFang SC;
        font-weight: 500;
        color: #13be9b;
        margin-right: 4px;
      }
      .count {
        font-size: 14px;
        font-family: PingFang-SC-Heavy, PingFang-SC;
        font-weight: 800;
        color: #0d0e10;
      }
      .grey {
        font-size: 12px;
        color: #9f9f9f;
      }
      .icon {
        width: 15px;
        height: auto;
        margin: 0 5px;
      }
    }
  }
  .previewArea {
    width: 635px;
    height: 100%;
    box-sizing: border-box;
    padding: 0 40px 0 20px;
    .header {
      height: 42px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      color: #242424;
      font-size: 12px;
      .dots {
        display: flex;
        align-items: center;
        .item {
          display: flex;
          align-items: center;
          margin-right: 27px;
          .dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            margin-right: 8px;
          }
        }
        .item:last-child {
          margin-right: 0;
        }
      }
    }
    .tableBox {
      .theader {
        display: flex;
        align-items: center;
        height: 32px;
        background: #efefef;
        .cols {
          width: 575px;
          display: flex;
          justify-content: space-around;
          font-size: 12px;
          font-family: PingFang-SC-Heavy, PingFang-SC;
          font-weight: 800;
          color: #242424;
        }
      }
      .tbody {
        .row {
          display: table;
          .date {
            display: table-cell;
            width: 60px;
            background-color: green;
          }
          .rowItem{
            display: table-cell;
            width: 143px;
            background-color:red;
          }
        }
      }
    }
  }
}
</style>
<style lang="less">
.ivu-modal-body {
  padding: 0;
}
.ivu-form .ivu-form-item-label {
  padding: 10px 0;
}
</style>
