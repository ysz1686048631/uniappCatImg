<!--
 * @Author: your name
 * @Date: 2021-06-04 09:54:28
 * @LastEditTime: 2021-06-04 10:14:02
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vscdeUniapp\uniss\src\pages\tabbar\tabbar.vue
-->
<template>
    <view>
          <uni-table-list
                    ref="unitable"
                    @handleclick="onhandleClick"
                    @scrolllower="scrollLower"
                    :top-num="3"
                    :list-height="500"
			 >
		  </uni-table-list>
    </view>
</template>

<script>
import uniTableList from '../../components/uni-tablelist/uni-tablelist';
export default {
    data(){
         return{
            lists:[
				 '首页',
				 '组件',
                 '组件'
			],
            infos:[
				 {
					title:'列表1',
					type:'测试',  
				 }, {
					title:'列表2',
					type:'测试',  
				 }, {
					title:'列表3',
					type:'测试',  
				 }, {
					title:'列表4',
					type:'测试',  
				 }, {
					title:'列表5',
					type:'测试',  
				 }, {
					title:'列表6',
					type:'测试',  
				 }, {
					title:'列表7',
					type:'测试',  
				 }
			]
         }
    },
    components:{
       uniTableList
    },
    onShow(){
         this.scrollLower(1);
    },
    methods:{
         onhandleClick(e){
               console.log(e)    
         },
         scrollLower(e){
                setTimeout(()=>{
					     this.$refs.unitable.initloadFun(false);
					     this.$refs.unitable.onConsolidatedData(this.infos);
				  },1000)
         }
    }

    
}
</script>

<style>

</style>