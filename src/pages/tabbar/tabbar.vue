<!--
 * @Author: your name
 * @Date: 2021-06-04 09:54:28
 * @LastEditTime: 2021-06-04 10:12:04
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vscdeUniapp\uniss\src\pages\tabbar\tabbar.vue
-->
<template>
    <view>
          <uni-table-bar
			      :list="lists" 
			 	  @change="onclickfun"
				  temp-height="510"
				  :active-index="1"
			   >
				      <view slot="temp1">
                              组件1
                       </view>
					  <view slot="temp2">
						      组件2
					  </view>
                      <view slot="temp3">
						      组件3
					  </view>
			   </uni-table-bar>
    </view>
</template>

<script>
import uniTableBar from '../../components/uni-tablebar/uni-tablebar';
export default {
    data(){
         return{
            lists:[
				 '组件1',
				 '组件2',
                 '组件3'
			]
         }
    },
    components:{
       uniTableBar
    },
    methods:{
         onclickfun(e){
              console.log(e);
         }
    }

    
}
</script>

<style>

</style>