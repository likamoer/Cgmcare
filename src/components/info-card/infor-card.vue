<template>
  <Card :shadow="shadow" :title="title" class="info-card-wrapper" :class="{'isLine': !isLine}">
    <div class="card_icon" slot="extra" >
      <Icon type="ios-add-circle-outline" @click="add" v-if="addShow" :size="iconSize" color="#333" />
      <Icon type="ios-arrow-dropright" @click="go" v-if="goShow" :size="iconSize" color="#333" />
    </div>
    <div class="content-con">
      <div class="right-area">
        <div>
          <slot></slot>
        </div>
      </div>
    </div>
  </Card>
</template>

<script>
import CommonIcon from '_c/common-icon'
import Icons from '_c/icons'
export default {
  name: 'InforCard',
  components: {
    CommonIcon,
    Icons
  },
  props: {
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
    }
  },
  computed: {
    leftWidth () {
      return `${this.left}%`
    },
    rightWidth () {
      return `${100 - this.left}%`
    }
  },
  methods: {
    add () {
      // 添加暴露事件
      this.$emit('add')
    },
    go () {
      // 进入暴露事件
      this.$emit('go')
    }
  }
}
</script>

<style lang="less">
.common{
  float: left;
  height: 100%;
  display: table;
  text-align: center;
}
.info-card-wrapper {
  border-radius: 8px;
}
.ivu-card-head {
    border-bottom: 0px !important;
  }
.size{
  width: 100%;
  height: 100%;
}
.middle-center{
  display: table-cell;
  vertical-align: middle;
}
.icon {
  margin-right: 10px;
  cursor: pointer;
}
.info-card-wrapper{
  .size;
  width: 100%;
  // overflow: hidden;
  .ivu-card-body{
    width: 100%;
    padding: 0 10px;
    .size;
  }
  .content-con{
    width: 100%;
    border-top: 1px solid #ccc;
    padding: 10px 0;
    .size;
    position: relative;
  }
}
.isLine {
  .content-con{
    width: 100%;
    border-top: 0px solid #ccc;
    padding: 10px 0;
    .size;
    position: relative;
  }
}
</style>
