<template>
	<view class="contents">
		<!-- tab 标签页 -->
		    <view class="tabbars">
		    	   <view class="tabbars-list"
				         :style="{color:color}"
				   >
							      <view 
								  v-for="(item,index) in list"
								  :key="index"
								   @tap="clickfuns(index)"
								   :class="['tabbars-list-item',{'active':indexs==index}]"
								   >
							      			{{ item }}			      
							      </view>
								  
						   </view>
		    	   <view class="tabbars-line"  :style="{width:`${lineW}px`,transform:`translateX(${indexleft}px)`,background:color}"></view>
		        </view>
					<view class="content-temp" :style="{height:`${tempHeight}px`}">
						  <swiper  :current="indexs"
						   @transition="onTransitionTab"
						   @animationfinish="onFinishTab"
						   @change="onChangeTab"
						   class="swiper"
						   >
						   <swiper-item
						   >
						   	<view class="swiper-item">  
														<!-- 由于slot不能绑定传值 所以标签页能使用规格有2，3，4 -->
													    <!-- slot1 -->
						   	  
								 <slot name="temp1"></slot>
						   	</view>
						   </swiper-item>
						   <swiper-item
						   >
						   	<view class="swiper-item">
						   								<!-- slot2 -->
						   	     <slot name="temp2"></slot>
						   	</view>
						   </swiper-item>
						   <swiper-item
						     v-if="3<=list.length"
						   >
						   	<view  class="swiper-item">
						   								<!-- slot3 -->
						   	     <slot name="temp3"></slot>
						   	</view>
						   </swiper-item>
						   <swiper-item
						    v-if="4<=list.length"
						   >
						   	<view class="swiper-item">
						   								<!-- slot4-->
						   	     <slot name="temp4"></slot>
						   	</view>
						   </swiper-item>
						   
						  </swiper>
					</view>
	</view>
</template>

<script>
	/**
	 * 
	 * 参数1 activeIndex  当前显示索引
	 * 参数2 list     数据
	 * 参数3 color    主题颜色
	 * 参数4 tempHeight 模板高度根据需求用户自行设置
	 *       autoload 自动加载
	 * 
	 * */
	export default {
		data() {
			return {
				lineW:0,    		  // 视口宽度
				indexs:0,   		 // 当前索引
				indexleft:0,  		// 滚动条需要移动的偏移量
				preleft:0,    	   // 上一次滚动 的距离
			}
		},
		props:{
			  activeIndex:{
				    type:Number,
				    default:()=>{
				    	 return 0;
				    }
			  },
			  // 数据
			  list:{
				   type:Array,
				   validator:(t)=>{
					    if(t.length<1 || t==[]){
							  throw Error('lists annot be empty！！！') 
						}
					    return t;
				   },default:()=>{
					    return [];
				   }
			  },
			  // 主题颜色
			  color:{
				  type:String,
				  default:()=>{
					   return '#007fff'
				  }
			  },
			  tempHeight:{
				  type:String,
				  default:()=>{
					   return '50'
				  }
			  }
		},
		mounted(){
			 let { activeIndex } = this;
			 this.indexs = activeIndex;
			// 初始化 获取 视口宽度
			 let view = uni.createSelectorQuery().in(this).select(".tabbars-list");
			 view.fields({
			   size: true,
			   scrollOffset: true
			 }, data => {
			   this.lineW = parseInt(data.width)/this.list.length;
			 }).exec();
		},
		methods: {
			// 点击标签页
			clickfuns(index){
				 this.indexs=index;
			},
			// 轮播改变调用事件
			onTransitionTab(e){
			// 本次移动距离=上次移动距离 + swiper移动的三分之一
				 this.indexleft=this.preleft+parseInt(e.detail.dx)/this.list.length;
			},
			// 保留上次距离
			onFinishTab(e){
			// this.allleft=0;
				 this.preleft=this.indexleft;
			},
			// swiper改变时调用
			onChangeTab(e){
				 let index = e.detail.current;
				 this.indexs=index;
				 this.onFeekback(index);
			},
			// 反馈事件
			onFeekback(index){
				 this.$emit('change',index); 
			}
		}
	}
</script>

<style lang="less" scoped>
.contents{
	 width: 100%;
	 .tabbars{
		  width: 100%;
		  &-list{
			  width: 100%;
			  height: 80upx;
			  display: flex;
			  flex-direction: row;
			  align-items: center;
			  justify-content: center;
			  border-top: 1upx solid #ccc;
			  border-bottom: 1upx solid #ccc;
			  color: #f40;
			  &-item{
				   flex: 1;
				   text-align: center;
				   font-size: 26upx;
				   font-weight: bold;
				   color: #666;
				   transition: .2s;
				   &.active{
					    color:currentcolor;
				   }
			  }
		  }
		  &-line{
			   height: 1px;
			   background: #f40;
			   
		  }
	 }
	 .swiper{
		  width: 100%;
		  height: 100%;
	 }
}
</style>
