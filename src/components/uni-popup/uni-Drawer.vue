<template>
	<!-- // 基础样式层 -->
	<view class="drawer" :style="{zIndex:!filterShowPop?'-9':1}">
		<view class="drawer_content">
			        <view class="drawer_content_overlay" :style="{opacity:!showpopups?0:1}" @tap="onHidePopus"></view>
		            <view :class="[
					   'drawer_content_silder',
				    ]"
				       :style="{
						   width:position=='left'||position=='right'?styles['width']:'100%',    
						   height:position=='top'||position=='bottom'?styles['height']:'100%',  
						   top:position=='top' && !showpopups?`-${styles['height']}`:'',        
						   bottom:position=='bottom' && !showpopups?`-${styles['height']}`:'',
						   left:position=='left' && !showpopups?`-${styles['width']}`:'',
						   right:position=='right' && !showpopups?`-${styles['width']}`:''
						   }"
				   >
				   <!-- // 左右  需要执行宽度 // 上下  需要指定高度  // 底部  是否展示  -->
					   <view class="content">
						       <slot></slot>
					   </view>
				</view>   
		</view>
	</view>
</template>
<script>
	
	// 弹窗popup  上 下 左 右
	export default {
		name:'uni-popup',
		props:{
			  // 是否展示
			  value:Boolean,
			  // 展示位置
			  position:{
				   type:String,
				   default:()=>{
					    return 'right';
				   }
			  },
			  // 样式  只能设置 height/width
			  styles:{
				   type:Object,
				   default:()=>{
					    return  {
							 width:'30%',
						};
				   }
			  },
			 
		},
		// #ifdef H5
		// 由于App端不支持 所以 将其归为H5端使用
		// model 主要用于 自定义组件同步改变父组件使用v-model传递过来的值
		// 通俗讲 主要用于 子组件更父组件中的属性（该属性必须被绑定到子组件中）
		model:{
			 prop:'value',
			 event:'changes'
		},
		// #endif
		
		watch:{
			 // #ifdef H5
			 value(newVal) {
				   this.showpopups=newVal;
				   setTimeout(()=>{
					    this.filterShowPop=newVal
				   },200)
			     },
			 // #endif	 
		},
	
		data() {
			return {
				  filterShowPop:this.value,
				  showpopups:this.value
			}
		},
		methods:{
		// #ifdef 
		// h5 端隐藏
			 onHidePopus(){
				 this.$emit('changes',false);
			 },
		// #endif 
		// #ifndef H5
		// 以下辅助函数H5端不可用
		// 隐藏弹窗
			onHidePopus(){
				  this.showpopups=false;
				  setTimeout(()=>{
				  		   this.filterShowPop=false;
				  },200)
			},
		//  展示弹窗 
			onShowPopus(){
				  this.showpopups=true;
				  setTimeout(()=>{
						   this.filterShowPop=true;
				  },200)

			}
		// #endif 
		}
	}
</script>
<style lang="less" scoped>
	.drawer{
		  position: fixed;
		  top: 0;
		  left: 0;
		  height: 100vh;
		  width: 100%;
		  z-index: 1;
		 &_content{
		 	 width: 100%;
		 	 height: 100vh;
		 	 position: relative;
			 &_overlay{
				 width: 100%;
				 height: 100%;
				 background:rgba(64, 65, 53, 0.3);
				 position: absolute;
				 left: 0;
				 top: 0;
				 opacity: 1;
				 transition: all .5s ease-in-out 0s; 
				 
			 }
		 	 &_silder{
		 		  width: 100%;
		 		  height: 100%;
		 		  background: #fff;
		 		  position: absolute;
		 		  left: 0;
		 		  top: 0;
		 		  bottom: 0;
		 		  right: 0;
		 		  overflow: hidden;
		 		  transition: all .3s ease-in-out 0s; 
		 		  // 如果想给某个 元素添加动画  那么这个元素 必须在css 样式中声明过
		 	 }
		 	 .content{
		 		  height:100%;
		 		  width: 100%;
		 	 }
		 }
	}
    
</style>
