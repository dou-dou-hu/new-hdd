<template>
  <div>
      <h5>排序翻页功能</h5>
      <p>
          <input placeholder="请输入" v-model="search" @input="searchShop">
      </p>
       <ul>
         <li>
             <h5>编号 <img src="../assets/arrow-red.png"  @click="upShop"/></h5>
         </li> 
         <li>
            <h5>名称</h5>
         </li>
         <li>
            <h5>价格 <img src="../assets/arrow-down.png"  @click="downShop"/></h5>
         </li>
        
       </ul>
        <ul v-for="item in sortList" :key="item.id">
            <li>
              <span>{{item.id}}</span>
            </li>
            <li>
              <span>{{item.goods_name}}</span>
            </li>
            <li>
              <span>{{item.price}}</span>
            </li>
       </ul>
       <div class="page">
          每页 <input type="text" v-model="num" @input="setPage">
           <li v-for="(item,index) in getPage" :key="index"><a href="#" @click="currentPage(item)">{{item}}</a></li>
       </div>
        
  </div>
</template>
 
 <script>
  //分页思路-1.每页多少条？数组slice(0,每页几条)  2.分多少页-Math.ceil(总数/1页几条) 3.点击当前页-传入当前页-找规律 0-2  3-5  6-8 进行截取数组slice(从第几开始,索引+每页个数)
 export default {
     name: 'Home',
     data() {
       return {
          shopList:[
            {
              "id": 1,
              "goods_name": "vivo 手机 p30",
              "price": 1242
            },
            {
              "id": 2,
              "goods_name": "苹果手机 iphone plus",
              "price": 45000
            },
            {
              "id": 3,
              "goods_name": "宝马 X7 4驱",
              "price": 750000
            },
            {
              "id": 4,
              "goods_name": "宝马 5系 2驱",
              "price": 450000
            },
            {
              "id": 5,
              "goods_name": "锤子手机 200G",
              "price": 2000
            },
            {
              "id": 6,
              "goods_name": "华为手机 P40",
              "price": 5000
            },
            {
              "id": 7,
              "goods_name": "红米 手机",
              "price": 1200
            },
            {
              "id": 8,
              "goods_name": "海尔电冰箱 3匹",
              "price": 980
            },
            {
              "id": 9,
              "goods_name": "苹果笔记本电脑 i9",
              "price": 20000
            },
            {
              "id": 10,
              "goods_name": "精品手机 华为 200G",
              "price": 3200
            }
          ],
          sortList:[],//排序数据
          search:'',//搜索词
          num:3, //每页几条
          page:4,//共几页
          total:10,//总数
       }
     },
     created() {
        this.sortList=this.shopList
     },
     computed:{
          //分多少页-总数/1页几条
           getPage(){
             this.page=Math.ceil(this.total/this.num)
             return this.page
           },
     },
     methods: {
       //搜索
       searchShop(){
          //注意是模糊匹配  
          this.sortList=[]
          this.shopList.forEach(item=>{
              if(item.goods_name.indexOf(this.search)!=-1){
                this.sortList.push(item)
              }
          })
          
       },
       //升序
        upShop(){
            this.sortList=this.shopList.sort((a,b)=>{
               return a.id-b.id
            })
            
        },
        //降序
        downShop(){
               this.sortList=this.shopList.sort((a,b)=>{
               return b.price-a.price
            })
        },
        //每页多少条-只显示第1页，每次改变时在触发
        setPage(){
           this.sortList=this.shopList.slice(0,this.num)
           
        },
        //点击当前页-传入当前页-规律 0-2  3-5  6-8 
        currentPage(item){
            let idx=(item-1)*this.num 
            let num=idx+Number(this.num)
            console.log(idx,num)
            this.sortList=this.shopList.slice(idx,num)
            
        }
     },
 }
          
 </script>
<style lang="less">
  html,body,#app {
        margin: 0;
        padding: 0px;
        height: 100%;
      }

  ul{
    display: flex;
    li{
      flex: 1;
      
    }
  }  
  .page{
    display: flex;
    li{
       margin-left: 30px;
    }
  }
</style>
