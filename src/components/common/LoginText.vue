<template>
  <div>
      <van-cell-group>
        
        <van-field
            v-model="content"
            :placeholder="placeholder"
            :label="label"
            :type="type"
            :rules="[{ pattern, message: '格式错误' }]"
        />
       
       </van-cell-group>
  </div>
</template>

<script>
export default {
    data() {
        return {
            content:'',
            pattern:eval(this.rule)
        }
    },
    mounted() {

    },
    props:['label','placeholder','type','rule'],
    watch:{
        content() {
               this.$emit('contentWatch',this.content)
        }
    }
}
</script>

<style>

</style>