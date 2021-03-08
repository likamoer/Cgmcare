<template>
  <div class="tab-table-select-page">
    <Card shadow class="info-card-wrapper">
      <div class="tab">
        <Tabs :value="name1">
          <TabPane :label="item.label" :name="item.value" v-for="(item, index) in tabDatas" :key="index"></TabPane>
          <div slot="extra">
            <Row type='flex' span="24" style="width: 600px" justify='space-around' :gutter='20'>
                <Col flex span="5" class="select">
                  <Select v-model="model1" style="width: 120px" placeholder="近三个月患者">
                    <Option v-for="item in cityList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                  </Select>
                </Col>
                <Col flex span="7" class="input">
                  <Input v-model="inputValue" placeholder="用户名/设备名称/设备编号" style="width: 180px" />
                </Col>
                <Col flex span="4" class="button">
                  <Button icon="ios-add">添加患者</Button>
                </Col>
                <Col flex span="3" class="icon">
                  <Icon type="ios-apps" :class="{'isActive': button == 1}" @click="changeButton(1)" />
                  <!-- <img src="../../assets/images/card.png" alt="" :class="{'isActive': button == 1}" @click="changeButton(1)">
                  <img src="../../assets/images/table.png" alt="" :class="{'isActive': button == 2}" @click="changeButton(2)"> -->
                  <Icon type="md-menu" :class="{'isActive': button == 2}" @click="changeButton(2)"  />
                </Col>
            </Row>
          </div>
        </Tabs>
      </div>
      <div class="tag">
        <div class="tag-con" v-for="(item, index) in tagDatas" :key="index" @click="changeStatus(item)" :class="{'isActive': item.active}">
          {{item.name}}<span v-if="item.num">({{item.num}})</span>
        </div>
      </div>
      <div class="table" v-if="button == 1">
        <Table
          :border='false'
          context-menu
          show-context-menu
          :loading="loading"
          :columns="columns1"
          :data="data1"
          @on-contextmenu="handleContextMenu">
          <template slot="contextMenu">
            <DropdownItem @click.native="handleContextMenuEdit">编辑</DropdownItem>
            <DropdownItem @click.native="handleContextMenuDelete" style="color: #ed4014">删除</DropdownItem>
          </template>
        </Table>
        <div class="page">
          <Page :total="100" show-sizer show-elevator show-total prev-text="上一页" next-text="下一页" />
        </div>
      </div>
      <div class="card" v-if="button == 2">
        <div class="card-item">
          <div class="item-top">
            <div class="top-left">
              <div class="name-age">
                <span class="name">王晓明</span>
                <span class="age">55岁</span>
                <span class="age">男</span>
              </div>
              <div class="time">
                3分钟前
              </div>
              <div class="measure">
                <div class="number-big">6.2</div>
                <div class="number-small">
                  <div class="small-top">
                    <div class="arrow">
                      <Icon type="md-arrow-round-up" />
                    </div>
                    <div class="number-add">+0.2</div>
                  </div>
                  <div class="small-measure">
                    mmol/L
                  </div>
                </div>
              </div>
            </div>
            <div class="top-right">
              <div class="image">
                <img src="../../assets/images/process.png" alt="">
                <div>正在监测</div>
              </div>
              <div class="unit">15床</div>
            </div>
          </div>
          <div class="item-middle">
            <chart-line style="height: 100px;" :value="pieData" text="患病类型">
            </chart-line>
            <!-- <div class="statistics">
              <div class="zhijian item-box">
                <div class="title">300次</div>
                <div class="sub_title">指尖血糖监测</div>
              </div>
              <div class="dongtai item-box">
                <div class="title">3周期</div>
                <div class="sub_title">动态血糖监测</div>
              </div>
            </div> -->
          </div>
          <div class="item-bottom">
            <div class="ku">
              <img src="../../assets/icons/ku.png" alt="">
              333克
            </div>
            <div class="u">
              <img src="../../assets/icons/u.png" alt="">
              12U
            </div>
            <div class="ci">
              <img src="../../assets/icons/ci.png" alt="">
              3次
            </div>
            <div class="kal">
              <img src="../../assets/icons/kal.png" alt="">
              1234千卡
            </div>
          </div>
        </div>
      </div>
    </Card>
  </div>
</template>

<script>
import CommonIcon from '_c/common-icon'
import { ChartLine } from '_c/charts'
export default {
  name: 'Screen',
  components: {
    CommonIcon,
    ChartLine
  },
  props: {
    tabDatas: {
      type: Array,
      default: () => [
        { label: '标签一', value: '0', active: false },
        { label: '标签二', value: '1', active: false },
        { label: '标签三', value: '2', active: false },
        { label: '标签四', value: '3', active: false }
      ]
    },
    tagDatas: {
      type: Array,
      default: () => [
        { name: '住院患者', num: 0, active: false },
        { name: '住院患者', num: 11, active: false },
        { name: '住院患者', num: 11, active: false },
        { name: '住院患者', num: 11, active: false }
      ]
    },
    addShow: {
      type: Boolean,
      default: true // 添加图片显隐
    },
    goShow: {
      type: Boolean,
      default: true // // 进入图片显隐
    },
    title: {
      type: String,
      default: '' // 图片标题
    },
    isLine: {
      type: Boolean,
      default: true // // 进入图片显隐
    },
    iconSize: {
      type: Number,
      default: 20 // icon大小
    },
    left: {
      type: Number,
      default: 20 // 左距离
    },
    shadow: {
      type: Boolean,
      default: false // 卡片是否有阴影
    },
    cityList: {
      type: Array,
      default: () => [
        { label: '标签一', value: 0, active: false },
        { label: '标签二', value: 1, active: false },
        { label: '标签三', value: 2, active: false },
        { label: '标签四', value: 3, active: false }
      ]
    }
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
      button: 1,
      name1: '2',
      inputValue: '',
      model1: '',
      loading: false,
      columns1: [
        {
          title: 'Name',
          key: 'name'
        },
        {
          title: 'Age',
          key: 'age'
        },
        {
          title: 'Address',
          key: 'address'
        }
      ],
      data1: [
        {
          name: 'John Brown',
          age: 18,
          address: 'New York No. 1 Lake Park',
          date: '2016-10-03'
        },
        {
          name: 'Jim Green',
          age: 24,
          address: 'London No. 1 Lake Park',
          date: '2016-10-01'
        },
        {
          name: 'Joe Black',
          age: 30,
          address: 'Sydney No. 1 Lake Park',
          date: '2016-10-02'
        },
        {
          name: 'Jon Snow',
          age: 26,
          address: 'Ottawa No. 2 Lake Park',
          date: '2016-10-04'
        }
      ]
    }
  },
  computed: {
  },
  methods: {
    changeButton (flag) {
      this.button = flag
    },
    changeStatus (item) {
      item.active = !item.active
    },
    handleContextMenu (row) {
      const index = this.data1.findIndex(item => item.name === row.name)
      this.contextLine = index + 1
    },
    handleContextMenuEdit () {
      this.$Message.info('Click edit of line' + this.contextLine)
    },
    handleContextMenuDelete () {
      this.$Message.info('Click delete of line' + this.contextLine)
    }
  }
}
</script>

<style lang="less">
.size {
  width: 100%;
  height: 100%;
}
.tab {
  .ivu-tabs {
    overflow: inherit !important;
  }
  .ivu-tabs-nav-right {
    position: relative;
  }
  .ivu-tabs-tab-active {
    color: #16CCA6 !important;
  }
  .ivu-tabs-tab-focused {

  }
  .ivu-tabs-ink-bar {
    background-color: #16CCA6;
  }
  .select {
    .ivu-select-selection {
      border: 0px !important;
    }
  }
  .button {
    button {
      border: 0px !important;
      font-size: 14px;
      font-family: PingFangSC-Regular, PingFang SC;
      font-weight: 400;
      color: #242424;
      line-height: 14px;
      outline: none;
    }
    .ivu-icon {
      font-size: 19px;
      font-weight: 700;
    }
  }
  .icon {
    display: flex;
    justify-content: flex-end;
    align-items: center;
    .ivu-icon {
      font-weight: 700;
      font-size: 20px;
      margin-left: 5px;
      color: #ccc;
    }
    .ivu-icon:last-child {
      font-size: 25px;
    }
    .isActive {
      color: #333 !important;
    }
  }
}
.tag {
  display: flex;
  width: 100%;
  .tag-con {
    padding: 3px 5px;
    font-size: 12px;
    font-family: PingFang-SC-Regular, PingFang-SC;
    font-weight: 400;
    color: #242424;
    line-height: 14px;
    width: auto;
    background: #eee;
    border-radius: 3px;
    margin-right: 10px;
  }
  .isActive {
    background: #16CCA6;
    color: #fff;
  }
}
.table {
  margin-top: 20px;
  width: 100%;
  .page {
    width: 100%;
    display: flex;
    justify-content: center;
    margin-top: 30px;
  }
}
.card {
  margin-top: 20px;
  .card-item {
    width: 259px;
    // height: 185px;
    border: 1px solid #E6E9F0;
    padding-bottom: 10px;
    border-radius: 6px;
    .item-top {
      display: flex;
      justify-content: space-between;
      padding: 10px 10px 0;
    }
    .top-left {
      .name-age {
        width: 100%;
        .name {
          font-size: 18px;
          font-family: PingFangSC-Semibold, PingFang SC;
          font-weight: 600;
          color: #000000;
          line-height: 20px;
        }
        .age {
          display: inline-block;
          margin-left: 5px;
          font-size: 12px;
          font-family: PingFangSC-Regular, PingFang SC;
          font-weight: 400;
          color: #9F9F9F;
          line-height: 14px;
        }
      }
      .time {
        font-size: 12px;
        font-family: PingFangSC-Regular, PingFang SC;
        font-weight: 400;
        color: #7A7A7A;
        line-height: 17px;
        margin: 3px 0;
      }
      .measure {
        display: flex;
        margin-top: 10px;
        .number-big {
          font-size: 38px;
          font-family: PingFangSC-Semibold, PingFang SC;
          font-weight: 600;
          color: #000000;
          line-height: 39px;
        }
        .number-small {
          position: relative;
          top: -7px;
          .small-top {
            display: flex;
            align-items: flex-end;
            .arrow {
              font-weight: 800;
              font-size: 20px;
              color: #000;
            }
          }
          .small-measure {
            font-size: 12px;
            text-align: right;
          }
        }
      }
    }
    .top-right {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      .image {
        // display: flex;
        text-align: center;
        img {
          width: 29px;
          height: 29px;
        }
        div {
          font-size: 12px;
          font-family: PingFangSC-Regular, PingFang SC;
          font-weight: 400;
          color: #BCBCBC;
          line-height: 10px;
        }
      }
      .unit {
        font-size: 15px;
        font-family: PingFangSC-Medium, PingFang SC;
        font-weight: 500;
        color: #242424;
        line-height: 18px;
        text-align: right;
        position: relative;
        top: -8px;
      }
    }
    .item-middle {
      height: 100px;
      width: 100%;
      .statistics {
        height: 100%;
        display: flex;
        background: #FCFCFC;
        justify-content: space-between;
        align-items: center;
        .item-box {
          flex: 1;
          display: flex;
          flex-direction: column;
          justify-content: center;
          align-items: center;
          .title {
            font-size: 12px;
            font-family: PingFangSC-Regular, PingFang SC;
            font-weight: 400;
            color: #242424;
            line-height: 13px;
          }
        }
      }
    }
    .item-bottom {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0 10px;
      div {
        display: flex;
        align-items: center;
        img {
          width: 16px;
          height: 16px;
        }
        font-size: 12px;
        font-family: PingFangSC-Regular, PingFang SC;
        font-weight: 400;
        color: #AAAAAA;
        line-height: 13px;
      }
    }
  }
}
</style>
