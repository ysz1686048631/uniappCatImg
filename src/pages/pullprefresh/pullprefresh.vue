<!--
 * @Author: your name
 * @Date: 2021-06-08 16:34:43
 * @LastEditTime: 2021-06-08 17:37:23
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \uniss\src\pages\pullprefresh\pullprefresh.vue
-->
<template>
     <view>
           <unipullprefresh
             :isloading="isloading"
             @endRefresh="endRefreshs"
           >
              <tabbar-temps
             :datas="datas"
			        type="theme1" 
            ></tabbar-temps>
                    <view class="texts">text</view>
                    <view class="texts">text</view>
                    <view class="texts">text</view>
           </unipullprefresh>
     </view>
</template>

<script>
import unipullprefresh from '../../components/uni-pulluprefresh/uni-pulluprefresh.vue';
import tabbarTemps from '../../components/tabbar-temps/tabbar-temps.vue';
export default {
   name:'prefresh',
   components:{
       unipullprefresh,
       tabbarTemps
   },
   data(){
        return{
             isloading:false,
                 datas:[
				    {
				       name:'新闻1' 
				    },{
				       name:'新闻2' 
				    },{
				       name:'新闻3' 
				    },{
				       name:'新闻4' 
				    },{
				       name:'新闻5' 
				    },{
				       name:'新闻6' 
				    },{
				       name:'新闻7' 
				    }
				],
        }
   },
   mounted(){
     
   },
   methods:{
      //  结束刷新
         endRefreshs(){
             this.isloading=true
             setTimeout(()=>{
                 this.isloading=false
            },500)
         }
   }
   
}
</script>

<style>
.texts{
     width: 100%;
     height: 100upx;
     line-height: 100upx;
     text-align: center;
}
</style>