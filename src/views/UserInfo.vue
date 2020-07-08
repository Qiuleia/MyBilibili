<template>
 <div class="userinfo">
      <navbar/>
      <img src="@/assets/bannerTop_new.png" alt="" class="backImg">
    <user-detail :userInfo="model"/>
    <user-article/>
  </div>
</template>

<script>
import navbar from '@/components/common/Navbar'
import userDetail from '@/components/usercomp/userDetail'
import userArticle from '@/components/usercomp/userArticle'
export default {
    data(){
        return{
            model:{}
        }
    },
    components:{
     navbar,
     userDetail,
     userArticle
    },
    methods:{
        async userData() {
            const res =  await this.$http.get('/user/' + localStorage.getItem('id'))
            this.model = res.data[0]    
        }
    },
    created() {
        this.userData()
    }
}
</script>

<style lang="less" scoped>
.userinfo{
.backImg{
    height: 91px;
    width: 100%;
}
}
</style>