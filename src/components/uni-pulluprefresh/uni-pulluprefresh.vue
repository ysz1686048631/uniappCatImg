<template>
	<view>
		  <view class="Pulluprefresh"
		   @touchstart="pageTouchstart"
		   @touchmove="pageTouchmove"
		   @touchend="pageTouchend"
		  >
					<view class="Pulluprefresh_loading" 
					  :style="{
						  height:`${startrefresh?defailtHeight:height}px`,
						  maxHeight:`${startrefresh?defailtHeight:height}px`,
						  transition:`${startrefresh?'0.3':pageTransition}s`}"
					>
						       <view class="image">
						       	     <image :class="[{'activeReady':startrefresh}]" :style="{transform: `rotate(${height}deg)`}" class="img" src="../../static/mao.svg" mode="widthFix"></image>
						       </view>
							   <view class="text">
							   	       {{ loadtext }}
							   </view>
							   <view class="bg">
							   	     <image  src="../../static/bgs.svg" mode="widthFix"></image>
							   </view>
					</view>
					<view class="Pulluprefresh_content"
					>
					   <slot></slot>
					</view> 	
		  </view> 
	</view>
</template>

<script>
	let windowHeight=0;
	export default {
		data() {
			return {
				startTop:0,       // 点击开始
				moveTop:0,		  // 点击移动
				endTop:0,		  // 点击结束
				height:0,
				pageTransition:0.3,
				defailtHeight:0,
				startrefresh:false,
				loadtext:'正在刷新...',
			}
		},
		props:{
			 //  背景只能使用图片来改变
			 bgurl:{
				  default:'#edf1f8'
			 },
			 // 加载动画 true 加载 false 结束加载
			 isloading:{
				  type:true,
				  default:()=>{
					   return false;
				  }
			 }  
		},
		watch:{
			isloading(n,o){
				 this.startrefresh = n;
			}  
		},
		mounted(){
			
			uni.getSystemInfo({
				success: function(e){
					windowHeight = e.windowHeight;
				}
			})
			this.defailtHeight = (windowHeight/6)*0.8;
			this.startrefresh=this.isloading;
		},
		methods: {
			// 滑动开始
			  pageTouchstart(e){
				      if(this.startrefresh){
						   return false;
					  }
					  this.loadtext='向下拉';
				      this.pageTransition=0;
					  this.startrefresh=false;
				      this.startTop = e.touches[0].pageY
			  },
			  // 滑动
			  pageTouchmove(e){
				     if(this.startrefresh){
				     	  return false;
				     }
				     this.pageTransition=0;
					 this.startrefresh=false;
				     this.moveTop = e.touches[0].pageY;
					 if(this.moveTop-this.startTop<0){
						this.height=0
						return false
					 }
					 if(parseInt(this.moveTop-this.startTop)*0.3>windowHeight/4.5){
						   this.height=this.height;
						   this.loadtext='松手刷新！';
					 }else{
						  
						   this.height=parseInt(this.moveTop-this.startTop)*0.3;
					 }
					 
			  },
			  // 滑动结束
			  pageTouchend(e){
				     if(this.startrefresh){
				     	 return false;
				     }
					 this.loadtext='正在刷新...'
				     this.pageTransition=0;
					 this.startrefresh=false;
					 //  滑动大于50就添加动画
				     if(this.moveTop-this.startTop>50){
						 this.pageTransition=0.3;
					 } 
				     this.onEndRefresh();
			  },
			 // 结束刷新
			 onEndRefresh(){
					if(this.height>windowHeight/10){
						    this.height=0;
						  	this.startrefresh=true;
							// 反馈
							this.$emit('endRefresh');
					}else{
						    this.height=0;
					}	 
			 },
		}
	}
</script>

<style lang="less" scoped>

.Pulluprefresh{
	 &_loading{
		  width: 100%;
		  height: 0upx;
		  overflow: hidden;
		  display: flex;
		  flex-direction: column;
		  justify-content: center;
		  align-items: center;
		  background: #edf1f8;
		  position: relative;
		  .bg{
			   position: absolute;
			   left: 0;
			   top: 0;
			   width: 100%;
			   height: 100%;
			   background: #edf1f8;
			   image{
				    width: 100%;
			   }
		  }
		  .image{
			   // #ifdef H5
			    margin-top: 10upx;
			   // #endif    
			   z-index: 99;
				.activeReady{
					 animation: rotates 1.5s linear infinite;
				}
				@keyframes rotates{
					 0%{
						 transform: rotate(0deg); 
					 }100%{
						  transform: rotate(360deg); 
					 }
				}
		  }
		  .text{
			   
			    margin-top: 10upx;
				  
			    z-index: 99;
		  }
		  &>view{
			   display: flex;
			   justify-content: center;
			   align-items: center;
			   font-size: 27upx;
			   color: #666;
			   image{
				   width: 70upx;
				   height: 70upx;
			   }
		  }
	 }
}
</style>
