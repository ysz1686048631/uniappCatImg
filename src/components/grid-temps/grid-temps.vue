<template>
	<view>
		<view :class="[
			  'grid-box',
			  {'column-five':colmns=='5'},
			  {'column-three':colmns=='3'}
		]">
			    <view class="grid-box-item"
				 v-for="(item,index) in dataList"
				 :key="index"
				 @tap="onHandleTap(index)"
				>
			    	     <view>
							 <image :class="round?'round':''" :src="item.img" mode="heightFix"></image>
						 </view>
			    	     <view>
							 <text :style="{color:`${textColor}`}">{{ item.name }}</text>
						 </view>
						 
			    </view> 
		</view>
	</view>
</template>

<script>
	// 九宫格 组件
	export default {
		props:{
			// 列数量
			colmns:{
				   type:String,
				   default:()=>{
						return '4';
				   }
			},
			// 文字颜色
			textColor:{
				   type:String,
				   default:()=>{
						return '#666';
				   }
			},
			// 数据
			dataList:{
				   type:Array,
				   default:()=>{
						return [];
				   }		   
			},
			// 圆形边角
			round:{
				 type:Boolean,
				 default:()=>{
						return false;
				 }
			}
			
		},
		methods:{
			// 点击事件
			onHandleTap(index){
				 this.$emit('handle-tap',index);
			}
		}
	}
</script>

<style lang="less" scoped>

			 .grid-box{
				  width: 100%;
				  display:grid;
				  grid-template-columns: repeat(4,1fr);
				  grid-row-gap: 22upx;
				  padding: 20upx 0;
				  &.column-three{
					   grid-template-columns: repeat(3,1fr);
				  }
				  &.column-five{
				  	   grid-template-columns: repeat(5,1fr);
				  }
				  &-item{
					   display: flex;
					   flex-direction: column;
					   align-items: center;
					   justify-content: center;
					   padding: 20upx 20upx;
					   box-sizing: border-box;
					   /* #ifndef H5 */
					    height:150upx;
					   /* #endif */
					   &>view:nth-of-type(1){
							height: 100%;
							border-radius: 15upx;
							padding: 20upx 20upx;
							box-sizing: border-box;
							box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.4);
						    image{
								height: 100%;
								width: 100%;
								
						    }
							&.round{
								 border-radius:50%
							}
							
					   }
					   &>view:nth-of-type(2){
						   margin-top:10upx;
							text{
								font-size: 26upx;
								color: #666;
							}
					   }
					   
				  }
				  
			 }
		
</style>
