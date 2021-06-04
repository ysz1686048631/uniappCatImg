<template>
	<view class="tablelist" :style="{height:`${listHeight}upx`}">
		  <view class="emptylist" v-if="loadlists">
		    	<uni-loading :loading="true"></uni-loading>
		  </view>
		  <!-- #ifdef APP-PLUS -->
		      <view 
			  class="tablelist-lists" 
			  :style="{height:`${listHeight*2}upx`}"
			  v-if="!loadlists"
			  >
		<!-- #endif -->
		<!-- #ifdef MP-WEIXIN -->
		      <view 
			  class="tablelist-lists" 
			  :style="{height:`${listHeight}px`}"
			  v-if="!loadlists"
			  >
		<!-- #endif -->
			  <view class="emptylist" v-if="datalist.length<1 && !loadlists">
			  	     暂无数据...
			  </view>
			  <scroll-view 
			  v-if="datalist.length>=1"
			  class="scrolly"  
			  :scroll-y="scroll"
			  lower-threshold="50px"
			  @scrolltolower="onScrolltolower"
			  >
		  	    <view class="tablelist-lists_item" 
				@click="handleClicks(index)"
				v-for="(item,index) in datalist"
				:key="index"
				:style="{background:index+1>topNum?'':`rgba(${206-(index*10)},${80+(index*50)},${109+(index*60)},0.2)`}"
				>
				<view class="order" :style="{color:index+1>topNum?'':randomColor(index)}"><text>{{ index+1 }}</text></view>
				<view>
					<view>{{ item.title }}</view>
					<view class="name" v-if="item.name" :style="{background:index+1>topNum?'':`rgba(${206-(index*10)},${80+(index*50)},${109+(index*60)},0.4)`}">{{ item.name }}</view>
					<view class="type" v-if="item.type" :style="{background:index+1>topNum?'':`rgba(${206-(index*10)},${80+(index*50)},${109+(index*60)},0.4)`}">{{ item.type }}</view>
				</view>
		  	    </view>
				<uni-loading :loading="loading"></uni-loading>
				<view class="empty" v-if="isempty">
					   已经到底了
				</view>
			</scroll-view>	
		  </view>
	</view>
</template>

<script>
	/**
	 * 参数1 topNum 
	 * 参数2 lists   --- 废弃 
	 * 事件1 handleClick 
	 * 使用该组件 需要将视口设置为100vh
	 * */
	let filtersColor = (index)=>{
				  return `rgb(${222-(index*10)},${20+(index*50)},${49+(index*60)})`;
			 }
	let timer = null;	
	import  uniLoading  from '../uni-loading/uni-loading';	 
	export default {
		data() {
			// 使用 属性 赋值函数
			return {
				  randomColor:(e)=>{
					   return filtersColor(e);
				  },
				  loading:false,
				  datalist:[],
				  isempty:false,
				  loadlists:true,
				  page:0,
			};
		},
		components:{
			 uniLoading
		},
		props:{
			 // top到多少级
			 topNum:{
				  type:Number,
				  default:()=>{
					   return 3;
				  } 
			 },
			 // 数据
			 lists:{
				  type:Array,
				  default:()=>{
					   return  [];
				  } 
			 },
			 // 高度
			 listHeight:{
				 type:Number,
				 default:()=>{
				 	 return  300;
				 } 
			 },
			 // 是否允许滚动
			 scroll:{
				  type:Boolean,
				  default:()=>{
				  	 return  true;
				  } 
			 }
		},
		
		methods:{
			 initloadFun(type){
				  this.loadlists=type;
			 },
			 // 初始化数据
			 initdatas(){
				  let { lists } = this;
				  this.datalist = lists;
			 },
			 // 反馈事件
			 handleClicks(index){
				  this.$emit('handleclick',index);
			 },
			 // 滑动到底部100px时触发事件
			 onScrolltolower(){
				 // 如果上次结果为空那 本次就不用去加载了
				 if(this.isempty) return false;
				 // 防抖
				 if(timer){
					 clearTimeout(timer);
					 timer=null
				 }
				 
				 this.loading=true;
				 this.$emit('scrolllower',this.page);
				 timer = setTimeout(()=>{
					  this.page = this.page+1;
				 },400)
				 
			 },
			 // 隐藏loading动画
			 hideload(){
				 this.loading=false; 
			 },
			 // 由父级 自动初始化传递数据
			 onConsolidatedData(data){
				 this.hideload();
				 if(data.length < 1 || data == []){
					this.isempty=true;
				 }else{ 
					this.datalist.push(...data);
				 }
				 
			 }
			
		}
	}
</script>

<style lang="less" scoped>
.scrolly{
 width: 100%;
 height:100%;
 
}
.empty{
	 width: 100%;
	 margin: 20upx 0;
	 text-align: center;
	 font-size: 26upx;
	 color: #666;
}
.emptylist{
	 width: 100%;
	 padding: 60upx 0;
	 text-align: center;
	 font-size: 26upx;
	 color: #666;
}
.tablelist{
	width: 100%;
	
	&-lists{
		  display: flex;
		  flex-direction: column;
		  padding: 0 10upx;
		  box-sizing: border-box;
		  &_item{
				font-weight: bold;
				font-size: 30upx;
				padding: 20upx 0;
				background: #fff;
				padding-left: 30upx;
				display: flex;
				align-items: center;
				margin:10upx 0;
				overflow: hidden;
				border-radius: 50upx 0 0 50upx;
				box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
				&>view:nth-of-type(1){
					   width: 70upx;
					   border-right: 1px solid #cacaca;
					   margin-right: 10upx;
					   text-align: center;
							 color: #666;
						&>text{
							 display: inline-block;
						
							 
						}
				}
				&>view:nth-of-type(2){
					  width: 100%;
					  font-size: 26upx;
					  display: flex;
					  justify-content: space-between;
					  align-items: center;
					  &>view:nth-of-type(1){
						    width:400upx;
							text-align: center;
							text-overflow: ellipsis;
							white-space: nowrap;
							overflow: hidden;
							line-height:50upx;
					  }
					  .name{
						     font-weight: 100;
						     color: #666; 
							 font-size: 23upx;
							 margin-right: 30upx;
							 padding: 10upx 10upx;
							 border-radius: 8upx; 
							
					  }
					  .type{
							 font-weight: 100;
							 color: #666; 
							 font-size: 23upx;
							 margin-right: 30upx;
							 padding: 10upx 10upx;
							 border-radius: 8upx; 
							 background: #F1F1F1;
					  }
				}
		  }
     }
}	
 
</style>
