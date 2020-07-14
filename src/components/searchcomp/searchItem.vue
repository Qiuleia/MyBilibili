<template>
  <div class="wrap">
    <div class="title">{{text}}</div>
    <div class="item-wrap">
     <van-button class="item" round hairline plain type="info"
      v-for="item in searchitem" :key="item.name"  @click="pathPush(item.id)">{{item.name}}</van-button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['text', 'searchitem'],
  methods: {
      pathPush(id){
           this.$router.push(/article/+id)
      }
  },
};
</script>

<style lang="less" scoped>
.wrap {
    background-color: #fff;
  .title {
    margin: 10px;
    padding-top: 10px;
    color: rgb(90, 91, 92);
  }
  .item-wrap{
      padding: 10px;
      display: flex;
      flex-wrap: wrap;
      .item{
          margin: 5px 10px;
      }
  }
}
</style>