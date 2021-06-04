<!--
 * @Author: your name
 * @Date: 2021-04-30 10:32:42
 * @LastEditTime: 2021-06-04 10:18:10
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vscdeUniapp\uniss\src\pages\index\index.vue
-->
<template>
      <view class="home_content">
		    <!-- <view class="home_content_cell">
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
			</view> -->
			<view>
			   <uni-table-bar
			      :list="lists" 
			 	  @change="onclickfun"
				  temp-height="510"
				  :active-index="0"
			   >
				      <view slot="temp1">
						    <view class="title">Utool-ui</view>
							<view class="direct">
								  <text>一款基于Uniapp组件库</text>
							</view>
					  </view>
					  <view slot="temp2">
						      <uni-table-list
							     ref="unitable"
								 @handleclick="onhandleClick"
								 @scrolllower="scrollLower"
								 :top-num="6"
								 :list-height="500"
							  >
							  </uni-table-list>
					  </view>
			   </uni-table-bar>
			</view> 
	  </view>
	
</template>

<script>
import uniTableBar from '../../components/uni-tablebar/uni-tablebar';
import uniTableList from '../../components/uni-tablelist/uni-tablelist';
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
			lists:[
				 '首页',
				 '组件'
			],
			infos:[
				 {
					title:'CatImg图片剪切',
					type:'uniapp组件',
					url:'../catimg/catimg'	   
				 },{
					title:'Popus弹窗',
					type:'uniapp组件',
					url:'../popus/popus',	   
				 },{
					title:'Swiper轮播图',
					type:'uniapp组件',
					url:'../swiper/index',	   
				 },{
					title:'Grid九宫格',
					type:'uniapp组件',
					url:'../grids/index',	   
				 },{
					title:'Topbar顶部标签',
					type:'uniapp组件',
					url:'../tabbars/tabbars'   
				 },{
					title:'Tabbar标签页',
					type:'uniapp组件',
					url:'../tabbar/tabbar',	   
				 },{
					title:'List列表',
					type:'uniapp组件',
					url:'../tablists/tablists',	   
				 }
			]
		    
	   }
  },
  components:{
			 uniTableBar,
			 uniTableList
		},
  mounted(){
	    
  },		
  methods:{
	//   页面跳转
	   
	   onhandleClick(e){
		   console.log(e);
		    uni.navigateTo({
				  	url:this.infos[e].url
				  })
	   },
	   // 传递数据    
	   scrollLower(e){
				  setTimeout(()=>{
					     this.$refs.unitable.initloadFun(false);
					     this.$refs.unitable.onConsolidatedData(this.infos);
				  },1000)
		},
	   	// 标签页 改变的时候 触发事件  
	   onclickfun(e){
				if(e==1){
					this.scrollLower(1);
				}
		},
  }
}
</script>

<style lang="less" scoped>
.title{
	  width: 100%;
	  text-align: center;
	  font-weight: bold;
	  color: #333;
	  margin-top: 100upx;
}
.direct{
	  width: 100%;
	  text-align: center;
	  color: #333;
	  margin-top: 100upx;
}
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