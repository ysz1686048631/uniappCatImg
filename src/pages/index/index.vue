<!--
 * @Author: your name
 * @Date: 2021-04-30 10:32:42
 * @LastEditTime: 2021-06-02 09:29:19
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vscdeUniapp\uniss\src\pages\index\index.vue
-->
<template>
      <view class="home_content">
		    <view class="home_content_cell">
				    <view class="home_conent_cell-title">
						  组件
					</view>
					<view class="home_conent_cell_list">
						   <view class="home_conent_cell_list_item"
						   v-for="(item,index) in datas"
						   :key="index"
						    >
							    <button size="mini" @click="tobackpage(item.url)">{{ item.name }}</button> 
							</view> 
					</view>
			</view>
			<view></view> 
	  </view>
	
</template>

<script>
export default {
  name:'home',
  data(){
	   return{
		    datas:[
				 {
					 url:'../catimg/catimg',
					 name:'图片剪切' 
				 },
				 {
					url:'../popus/popus',
					name:'弹窗'  
				 },
				  {
					url:'../swiper/index',
					name:'轮播图'  
				 },{
					url:'../grids/index',
					name:'九宫格'  
				 },{
					url:'../tabbars/tabbars',
					name:'顶部标签'  
				 }
			],
		    
	   }
  },
  methods:{
	   tobackpage(src){
		   uni.navigateTo({
				  	url:src
				  })
	   }
  }
}
</script>

<style lang="less" scoped>
     .home_content{
		    width: 100%;
			padding: 20upx 20upx;
			box-sizing: border-box;

			&_cell{
				  display: flex;
				  flex-direction: column;
				 
				  &>view:nth-of-type(1){
					   font-size: 26upx;
					    padding: 20upx 0;
					   font-weight: bold;
					   
				  }
			}
	 } 
</style>