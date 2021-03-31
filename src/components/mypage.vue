<template>
  <div id=''>
<div>1</div>
 </div>
</template>

<script>
export default {
components: {
//定义 组件
  },
  data() { 
//接受数据      
    return {}
  },
mounted() {
//挂载后 进入页面加载
  },    
  created() {

  },
  methods:{
//方法 函数

  },
filters: {
//过滤，筛选
},
computed: {
//计算
},
//监听
watch: {
//被监听者名称
route: {
//是否一进入页面就开始监听
 immediate: false, 
//执行函数
handler(newVal, oldVal) {},
//是否深度监听
deep: false,
},
},
 }
</script>

<style scoped lang='scss'>
</style>