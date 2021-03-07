<template>
  <div class="company-page">
    <!-- 组织管理页面 -->
    <Card shadow>
      <div class="company-box">
        <Tabs :value="name1">
          <TabPane :label="item.label" :name="item.value" v-for="(item, index) in tabDatas" :key="index"></TabPane>
          <div slot="extra">
            <Row type='flex' span="12" style="width: 600px" justify='space-around' :gutter='20'>
                <Col flex span="6" class="input">
                  <Input v-model="inputValue" placeholder="用户名/设备名称/设备编号" style="width: 180px" />
                </Col>
                <Col flex span="3" class="button">
                  <Button icon="ios-add">新建部门</Button>
                </Col>
                <Col flex span="3" class="button">
                <Button icon="md-contacts">新建成员</Button>
                </Col>
            </Row>
          </div>
        </Tabs>
      </div>
      <div class="table">
        <Table
          :border='false'
          context-menu
          show-context-menu
          :loading="loading"
          :columns="columns1"
          :data="data1"
          @on-contextmenu="handleContextMenu">
        </Table>
      </div>
    </Card>
  </div>
</template>

<script>
export default {
  name: 'index_page',
  components: {
  },
  data () {
    return {
      name1: '1',
      tabDatas: [
        { label: '部门管理', value: '0', active: false },
        { label: '成员管理', value: '1', active: false }
      ],
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
  methods: {
    handleContextMenu () {}

  }
}
</script>
<style lang="less">
  .size {
    width: 100%;
    height: 100%;
  }
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
  .search-bar {
    width: 100%;
    display: flex;
    justify-content: space-between;
    border-bottom: 1px solid #ddd;
    padding-bottom: 20px;
  }
  .table {
    margin-top: 20px;
  }
  .button-add {
    button {
      border: 0px !important;
      outline: none !important;
      i {
        font-size: 20px;
        font-weight: 800;
      }
    }
  }
</style>
