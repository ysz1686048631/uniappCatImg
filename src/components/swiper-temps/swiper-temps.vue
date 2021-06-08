<template>
	<view class="swiperDom">
		<!-- 二次封装Swiper 动态改变行内样式 不能使用upx 作为单位只能是px/rpx-->
		   <swiper  
		   class="swiper"  
		   previous-margin="45px" 
		   next-margin="45px" 
		   :interval="interval"
		   circular
		   autoplay
		   @change="onChangeNum"
		   :style="'height: '+height+'px'"
		   >
			    <swiper-item 
				v-for="(item,index) in list" 
				:key="index"
				>
					 <view class="items" @tap="onHandleTap(item.url)">
					 	     <image 
							 :src="item.img" 
							 mode="widthFix"
							 :class="[activeIndex==index?'active':'']"
							 ></image>
					 </view>  
				</swiper-item> 
				
		   </swiper> 
		   <!-- #ifdef APP-PLUS || MP-WEIXIN -->
		   <view class="dot" v-if="showdot">
		   	      <view class="dot-list"
				  :style="{color:`${dotActiveColor}`}"
				  >
		   	      	   <view class="dot-list-item"
					    v-for="(item,index) in list"
					    :key="index+Math.random()"
						:class="[activeDot==index?'active':'']"
					   >
		   	      	   </view>
		   	      </view> 
		   </view>
		     <!-- #endif -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				activeIndex:0, // 当前选中的图片索引
		        activeDot:0,   // 当前指示点的索引
			}
		},
		props:{
			// 轮播时间间隔
			 interval:{
				  type:String,
				  default:()=>{
					   return '1500';
				  } 
			 },
			 // 当前选中的指示点颜色
			 dotActiveColor:{
				  type:String,
				  default:()=>{
					   return '#f40';
				  } 
			 },
			 // 当前高度
			 height:{
				  type:String,
				  default:()=>{
				   return '160';
				  } 
			 },
			 // 是否展示指示点
			 showdot:{
				  type:Boolean,
				  default:()=>{
				   return true;
				  } 
			 },
			 // 数据列表
			 list:{
				  type:Array,
				  default:()=>{
				     return [];
				  } 
			 }
			 
		},
	
		methods:{
			// 轮播图点击事件
			onHandleTap(e){
				   this.$emit('handle-tap',e);
			},
			
			// 改变轮播图
			onChangeNum(e){
				  this.activeIndex = e.detail.current;	
				  this.activeDot = e.target.current
			},
					
		}
	}
</script>

<style lang="less" scoped>
 .swiperDom{
	  width: 100%;
	  display: inline-block;
	  overflow:hidden;
 }
 .swiper{
	   width: 100%;
	   height: 100%;
	   display: flex;
	   justify-content: center;
	   align-items: center;
	   padding: 5upx 0;
	   .items{
		    width: 100%;
			text-align: center;
			padding: 0 1upx;
			box-sizing:border-box;
			image{
				  width: 100%;
				  border-radius: 15upx;
				  transform:scale(.8);
				  transition:all .2s ease-in-out 0s;
				  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.5);
				  filter:blur(1px);
				   /* #ifdef APP-PLUS || MP-WEIXIN || H5 */
					  &.active{
							transform:scale(1);
							filter:blur(0px);
					   }
				   /* #endif */
				 
			}
			
	   }
 }
 .dot{
	  width: 100%;
	   display: flex;
	   align-items: center;
	   justify-content: center;
	   &-list{
		   width: 100%;
		    display: flex;
		    align-items: center;
		    justify-content: center;
			&-item{
				  width: 25upx;
				  height: 7upx;
				  background:#ccc;
				  margin: 5upx 10upx;
				  border-radius: 5upx;
				  &.active{
					   background:currentcolor;
				  }
			}
	   }
 }

</style>
