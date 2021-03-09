<template>
  <div class="mealsPlan">
    <div class="header">
      <div class="title">早餐方案</div>
      <div class="nutrition">
        <span>碳水:33g</span>
        <span>蛋白质:123g</span>
        <span>脂肪:231g</span>
      </div>
    </div>
    <div class="foodList">
      <div class="foodItem" v-for="i in 10" :key="i">
        <p class="name">米饭</p>
        <p class="weight">110g</p>
        <Icon class="del" type="ios-trash-outline" />
      </div>
      <div class="foodItem">
        <Icon style="font-size:30px;color:#D8D8D8;" type="md-add"/>
      </div>
    </div>
    <div class="remark">
      备注：<Input style="width:200px" type="text" v-model="remark" placeholder="添加备注" maxlength="80"/>
    </div>
  </div>
</template>
<script>
export default {
  data: function () {
    return {
      remark: '',
      disable: true
    }
  }
}
</script>
<style lang="less" scoped>
.mealsPlan{
  box-sizing: border-box;
  padding: 15px 0 10px 10px;
  border-bottom: 1px solid #f4f4f4;
  .header{
    display: flex;
    align-items: center;
    justify-content: space-between;
    .title{
      height: 18px;
      font-size: 13px;
      font-family: PingFang-SC-Heavy, PingFang-SC;
      font-weight: 800;
      color: #242424;
    }
    .nutrition{
      color: #9F9F9F;
      font-size: 12px;
      display: flex;
      span{
        margin-left: 20px;
      }
    }
  }
  .foodList{
    margin-top: 12px;
    display: flex;
    flex-wrap: wrap;
    .foodItem{
      width: 85px;
      height: 44px;
      border-radius: 5px;
      border: 1px solid #E6E9F0;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 12px;
      flex-wrap: wrap;
      position: relative;
      margin:0 18px 17px 0;
      .name{
        width: 80%;
        text-align: center;
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        color: #242424;
      }
      .weight{
        color: #9F9F9F;
      }
      .del{
        font-size: 20px;
        position: absolute;
        right: -8px;
        top: -8px;
      }
    }
    .foodItem:nth-child(5n){
      margin-right: 0;
    }
  }
  .remark{
    font-size: 12px;
    font-family: PingFang-SC-Bold, PingFang-SC;
    font-weight: bold;
    color: #242424;
    display: flex;
    align-items: center;
  }
}
</style>
