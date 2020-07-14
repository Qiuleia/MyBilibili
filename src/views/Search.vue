<template>
  <div>
    <van-search v-model="value" show-action label="视频" placeholder="请输入搜索关键词" @search="onSearch">
      <template #action>
        <div @click="onBack">取消</div>
      </template>
    </van-search>
    <searchItem :text="text" :searchitem="item" />
    <searchItem v-if="historyItem" :text="history" :searchitem="historyItem" />
  </div>
</template>

<script>
import searchItem from "@/components/searchcomp/searchItem.vue";
export default {
  data() {
    return {
      value: null,
      text: "推荐",
      history: "历史记录",
      item: [
        { name: "一人之下", id: 7 },
        { name: "大理石日志", id: 8 },
        { name: "咬人猫", id: 11 },
        { name: "舞小猫", id: 12},
        { name: "老番茄", id: 13 },
        { name: "TheShy", id: 14 },
        { name: "罗翔老师", id: 16 },
        { name: "何同学", id: 17 },
        { name: "过山车", id: 18},
        { name: "新番吐槽", id: 3 },
        { name: "干物妹", id: 4 },
        { name: "粉彩回忆", id: 5 },
        { name: "Re:Stage", id: 6 },
        { name: "洛天依", id: 2 },
        { name: "Rap God", id: 9 },
      ],
      historyItem: []
    };
  },
  components: {
    searchItem
  },
  created() {
    this.getHistory();
  },
  methods: {
    onSearch() {
      if (this.value != "") {
        this.$router.push({
          path: "/article/" + 21,
          query: {
            name: this.value
          }
        });
        let data = localStorage.getItem("history") || [];
        if (!(data instanceof Array)) {
          data = JSON.parse(data);
        }
        data.unshift({
          name: this.value,
          id: 21
        });
        data = JSON.stringify(data);

        localStorage.setItem("history", data);
        this.getHistory();
      }
    },
    getHistory() {
      let data = localStorage.getItem("history") || [];
      if (!(data instanceof Array)) {
        data = JSON.parse(data);
      }
      this.historyItem = data;
    },
    onBack(){
      this.$router.back(-1)
    }
  }
};
</script>

<style>
</style>