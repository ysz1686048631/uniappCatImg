<template>
	<view class="catimgpage">
		<!-- 微信圆形头像 -->
		<h3>微信原型头像剪切组件（未封装）</h3>
		<!-- 剪切图片 -->
		     <view class="catimgpage-catimg">
					<view class="catimgpage-catimg_canvas">
						  <canvas 
						  @touchstart="onTouchstart"
						  @touchmove="onTouchMove" canvas-id="firstimg" id="firstimg"
						  style="width:100%;height:100%;"
						  ></canvas>
					</view>
					<!-- <view class="catimgpage-catimg_btn">选择图片</view> -->
			 </view>
		<!-- 样式图片 -->	 
		     <view class="catimgpage-showimg">
				       <canvas canvas-id="soencedimg" id="soencedimg" style="width:100%;height:100%;"></canvas> 
			 </view>
	    <!-- 点击按钮 -->
			 <view class="btn">
				   <button type="default" @tap="onCatimgFun">保存图片</button>
			 </view>	 
	</view>
</template>

<script>
	export default {
		data() {
			return {
				endtap:{
					 x:0,
					 y:0
				 },
				 starttap:{
					 x:0,
					 y:0
				 },
				 clients:{},
				 height:220, // 容器 + 图片大小
				 width:220,
				 arc:70
			}
		},
		mounted(){
		    this.onCilpimg(110,110);
		},
		methods: {
			// 保存剪切后的图片
			onCatimgFun(){
				 uni.canvasToTempFilePath({
				   canvasId:'soencedimg',
				   success: function(res) {
				     // 在H5平台下，tempFilePath 为 base64
					 console.log(res.tempFilePath);
					    let _t = this;
					   uni.saveImageToPhotosAlbum({
					   				 filePath:res.tempFilePath, //仅为示例，并非真实的资源
					   				 success: (res) => {
					   						   uni.showToast({
					   						   	   title:'保存成功的'
					   						   })
					   				  }
					   		      });
							
				   
				   } 
				 })
			},
			// 手触摸时候 记录位置
			onTouchstart(e){
				    this.starttap = e.touches[0];
					//获取 鼠标到 图片 边界位置
					let x = this.starttap.x-this.endtap.x;
					let y = this.starttap.y-this.endtap.y;
					this.clients={
						 x,
						 y
					}
				 
			},
		    // 移动的时候 变换位置 
			onTouchMove(e){
				  // console.log(this.endtap)
				  let taps = e.touches[0];
				  let x = taps.x-this.clients.x;// 圆环到边界的距离
				  let y = taps.y-this.clients.y;
				  console.log(y+this.arc,y);
				  if(x-this.arc<0){
					   x = this.arc;
				  }
				  else if(x+this.arc>this.height){
				  	   x = 10+(this.arc*2); 
				  }
				  // 鼠标点击的位置 - 半径 = 圆环的到顶部的距离
				  if(y-this.arc<0){
					   y = this.arc; 
				  }else if(y+this.arc>this.height-20){
					   y = (this.arc*2)-10; 
				  }
				  this.onCilpimg(x,y);
			},
			 showImg(x,y){
				  var ctx = uni.createCanvasContext('soencedimg');
				  //通过 触碰 设置 image的 位置
				 
				  // Draw arc
				  ctx.save();
				
				    // 绘制 截切 图形
				  ctx.arc((this.height/2),(this.width/2),this.arc, 0, 2 * Math.PI);
				
				 
				  ctx.clip(); // cilp 后都是 被剪切的 内容
				  ctx.setStrokeStyle('#ebeb00');
				  ctx.stroke()                      // 整个 盒子宽度 - 半径 - 移动的距离 = 图片视口位置
				  ctx.drawImage('../../static/logo.png',180-this.arc-x,180-this.arc-y,this.height,this.width);
				  
				  ctx.draw(true);
				 
			 },
			 onCilpimg(x,y){
				this.showImg(x,y); 
				 // 保存 图片节点右上角，x坐标 和 y坐标
				this.endtap = {
					 x,y
				}
				var ctx = uni.createCanvasContext('firstimg');
				//通过 触碰 设置 image的 位置
				ctx.drawImage('../../static/logo.png',0,0,this.height,this.width);
				// Draw arc
				ctx.beginPath();
				ctx.arc(x,y,this.arc, 0, 2 * Math.PI)
			
				ctx.setStrokeStyle('#ebeb00');
				ctx.stroke()
				
				ctx.restore();
				ctx.draw()
			 }
		}
	}
</script>
<style>
.catimgpage-catimg_canvas{
	   width: 100%;
	   height: 500upx;
}
.catimgpage-showimg{
	   width: 100%;
	   height: 500upx;
}
</style>

