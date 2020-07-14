<template>
  <div>
    <login-top text="注册bilibili">
      <div slot="right" style="font-size:3.611vw" @click="$router.push('/login')">用户登录</div>
    </login-top>
    <van-form validate-first>
    <login-text
      label="姓名"
      style="margin:15.001px 0;"
      placeholder="请输入(2-8位字)姓名"
     rule=/.{2,8}/
      @contentWatch="res => model.name = res"
    ></login-text>

    <login-text label="账号" 
         placeholder="请输入（4-8位字母数字）账号" 
        rule=/[\d|\w]{4,8}/
          @contentWatch="res => model.username = res"
    ></login-text>
    <login-text label="密码" 
            placeholder="请输入（4-8位字母数字）密码" 
            type="password"
            rule=/[\d|\w]{4,8}/
            @contentWatch="res => model.password = res"
    ></login-text>
    <login-btn BtnText="注册" @TextClick="AjaxInsert"/>
     </van-form>
  </div>
</template>

<script>
import loginTop from "@/components/common/LoginTop";
import loginText from "@/components/common/LoginText";
import loginBtn from "@/components/common/LoginBtn";
export default {
  data() {
    return {
      model:{
          name:"",
          username:"",
          password:""
      }  
    };
  },
  methods: {
    
       async AjaxInsert() {
            
            if(/.{2,8}/.test(this.model.name) && /[\d|\w]{4,8}/.test(this.model.username)&& /[\d|\w]{4,8}/.test(this.model.password)){
                const res =  await this.$http.post('/register',this.model)
                this.$msg.fail(res.data.msg)
                localStorage.setItem('token',res.data.objtoken) 
                localStorage.setItem('id',res.data.id) 
                setTimeout(() => {
                    this.$router.push('/userinfo')
                },2000)
            }else{
                this.$msg.fail('格式不正确,请重新输入!')
            }
        }
    
  },
  components: {
    loginTop,
    loginText,
    loginBtn
  }
};
</script>

<style lang="less" scoped>
</style>