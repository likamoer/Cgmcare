<template>
  <div class="monitor-page">
    <!-- 我的团队页面 -->
    <Card shadow>
      <div class="search-bar">
        <div class="input-search">
          <Input v-model="value" placeholder="用户名..." style="width: 300px" />
        </div>
        <div class="button-add">
          <Button icon="ios-add">添加患者</Button>
        </div>
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
