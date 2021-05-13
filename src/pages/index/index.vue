<template>
      <view class="home_content">
		    <view class="home_content_cell">
				    <view class="home_conent_cell-title">
						  组件
					</view>
					<view class="home_conent_cell_list">
						   <view class="home_conent_cell_list_item">
							    <button size="mini" @click="tobackpage(catSrc)">图片剪切</button> 
							</view> 
							 <view class="home_conent_cell_list_item">
							    <button size="mini" @click="tobackpage(popSrc)">弹窗啊</button> 
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
		    catSrc:'../catimg/catimg',
			popSrc:'../popus/popus' 
	   }
  },
  methods:{
	   tobackpage(src){
		   console.log(src);
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