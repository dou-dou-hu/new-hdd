<template>
       <div>
        <h5>分步表单</h5>
         <ul>
           <li>第一步</li>
           <li>第二步</li>
           <li>第三步</li>
           <li>第四步</li>
         </ul>
         <ul ref="tab">
            <div style="display:block" >
               商品名称：<input type="text" placeholder="请输入" v-model.trim="form.shop"><br>
                 <button @click="go">下一步</button>
            </div>
            <div >
               价格：<input type="text" placeholder="请输入" v-model.trim="form.price"><br>
                 <button @click="go">下一步</button>
            </div>
            <div>
               图片路径：<input type="text" placeholder="请输入" v-model.trim="form.img"><br>
                 <button @click="go">下一步</button>
            </div>
             <div>
               库存量：<input type="text" placeholder="请输入" v-model.trim="form.stock"><br>
                 <button @click="go">提交</button>
            </div>
         </ul>
         <div v-if="idx>3">
              商品展示：
             <li>商品：{{form.shop}}  </li>
             <li>价格：{{form.price}}  </li>
             <li>图片路径：{{form.img}}  </li>
             <li>库存量：{{form.stock}}  </li>
         </div>
      </div> 
</template>
<script>
//总的思路-1.点击下一步时，索引++，当前索引显示，其它的隐藏 2.提交时要用到存储的数据-可以对数据双向绑定
export default {
    data() {
        return {
            //索引-控制每步显示
            idx:0,
            //提交表单内容
            form:{
              shop:'',
              price:'',
              img:'',
              stock:'',
            }
        }
    },
    methods:{
       //点击下一步,判断当前是否为空。
       go(){
          if (this.idx === 0 && this.form.shop === '') {
              alert('商品名称不能为空！')
              return
          }
          if (this.idx === 1 && this.form.price === '') {
              alert('商品名称不能为空！')
              return
          }
          if (this.idx === 2 && this.form.img === '') {
              alert('商品名称不能为空！')
              return
          }

           this.idx++
           if(this.idx>3) return
           
           let arrDiv=this.$refs.tab.querySelectorAll('div')
           console.log([...arrDiv]); //转为真正数组，遍历
           for (const key in [...arrDiv]) {
              arrDiv[key].style.display='none'
           }
           
            arrDiv[this.idx].style.display='block'
           
       }
    }
}
</script>
<style lang="less">
    ul{
       li{
          display: flex;
       }
       div{
         display: none;
       }
    }
        
</style>