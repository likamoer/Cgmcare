<template>
  <div class="xuetang-page">
    <div class="page-header">
      <div class="image-logo">
        <img src="../../../assets/images/process.png" alt="">
      </div>
      <div class="title">
        监测设备：雅培瞬感I代
      </div>
      <div class="title">
        状态：已进行5天
      </div>
      <div class="title">
        管理开始时间：2020-11-10 20:20:20
      </div>
      <div class="title">
        管理结束时间：2020-11-10 20:20:20
      </div>
    </div>
    <div class="time">
      {{time1}}
    </div>
    <div class="data-analy">
      <div class="number">
        <div class="big">12.8</div>
        <div class="unit">
          <div class="arrow">
            <!-- <Icon type="md-arrow-round-up" /> -->
            <Icon type="md-arrow-round-down" />
          </div>
          <div class="unit-s">
            mmol/L
          </div>
        </div>
      </div>
      <div class="classify">
        <div class="item">
          <div class="icon-title">
            <img src="../../../assets/icons/u.png" alt="">
            <span>碳水</span>
          </div>
          <div class="sum">190g</div>
        </div>
        <div class="item">
          <div class="icon-title">
            <img src="../../../assets/icons/ku.png" alt="">
            <span>胰岛素</span>
          </div>
          <div class="sum">
            16U
          </div>
        </div>
        <div class="item">
          <div class="icon-title">
            <img src="../../../assets/icons/ci.png" alt="">
            <span>口服药</span>
          </div>
          <div class="sum">
            -.-
          </div>
        </div>
        <div class="item">
          <div class="icon-title">
            <img src="../../../assets/icons/kal.png" alt="">
            <span>运动</span>
          </div>
          <div class="sum">
            1221kcal
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Tables from '_c/tables'
import { getTableData } from '@/api/data'
export default {
  name: 'tables_page',
  components: {
    Tables
  },
  data () {
    return {
      time1: '3分钟前更新  14:35',
      columns: [
        { title: 'Name', key: 'name', sortable: true },
        { title: 'Email', key: 'email', editable: true },
        { title: 'Create-Time', key: 'createTime' },
        {
          title: 'Handle',
          key: 'handle',
          options: ['delete'],
          button: [
            (h, params, vm) => {
              return h('Poptip', {
                props: {
                  confirm: true,
                  title: '你确定要删除吗?'
                },
                on: {
                  'on-ok': () => {
                    vm.$emit('on-delete', params)
                    vm.$emit('input', params.tableData.filter((item, index) => index !== params.row.initRowIndex))
                  }
                }
              }, [
                h('Button', '自定义删除')
              ])
            }
          ]
        }
      ],
      tableData: []
    }
  },
  methods: {
    handleDelete (params) {
      console.log(params)
    },
    exportExcel () {
      this.$refs.tables.exportCsv({
        filename: `table-${(new Date()).valueOf()}.csv`
      })
    }
  },
  mounted () {
    getTableData().then(res => {
      this.tableData = res.data
    })
  }
}
</script>

<style lang='less' scoped>
.size {
  width: 100%;
  height: 100%;
}
.xuetang-page {
  width: 100%;
}
.page-header {
  width: 100%;
  height: 34px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
  background: #F7F7F7;
  border-radius: 1px;
  .image-logo {
    width: 28px;
    height: 28px;
    margin-right: 10px;
    margin-left: 5px;
    img {
      .size;
    }
  }
  .title {
    margin-right: 20px;
    font-size: 12px;
  }
}
.time {
  font-size: 15px;
  font-family: PingFangSC-Regular, PingFang SC;
  font-weight: 400;
  color: #9F9F9F;
  line-height: 23px;
  margin-top: 20px;
}
.data-analy {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .number {
    display: flex;
    align-items: center;
    .big {
      font-size: 64px;
      font-family: PingFangSC-Medium, PingFang SC;
      font-weight: 500;
      color: #242424;
      line-height: 89px;
      margin-right: 12px;
    }
    .unit {
      .arrow {
        font-size: 32px;
        color: #242424;
        text-align: center;
      }
      .unit-s {
        font-size: 15px;
        font-family: PingFangSC-Regular, PingFang SC;
        font-weight: 400;
        color: #9F9F9F;
        line-height: 23px;
        position: relative;
        top: -10px;
      }
    }
  }
  .classify {
    display: flex;
    .item {
      width: 100px;
      margin-left: 30px;
      text-align: center;
      .icon-title {
        display: flex;
        height: 30px;
        align-items: center;
        justify-content: center;
        span {
          display: inline-block;
          margin-left: 3px;
        }
      }
      .sum {
        width: 100%;
        text-align: center;
        font-size: 22px;
        font-family: PingFangSC-Semibold, PingFang SC;
        font-weight: 600;
        color: #242424;
        line-height: 32px;
      }
    }
  }
}
</style>
