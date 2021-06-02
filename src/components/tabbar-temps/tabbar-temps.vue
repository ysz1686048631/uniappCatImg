<!--
 * @Author: your name
 * @Date: 2021-06-02 09:21:03
 * @LastEditTime: 2021-06-02 14:21:22
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vscdeUniapp\uniss\src\components\tabbar-temps\tabbar-temps.vue
-->
<template>
       <view class="tabs">
            <scroll-view 
            scroll-x="true"
            class="scrollx"
			id="scrollx"
            show-scrollbar="false"
            scroll-with-animation
            :scroll-left="offestLeft"
            >
                  <view class="tabs-list-item"
                  
                  v-for="(item,index) in datas"
                  :key="index"
                  @tap="handleClick(index)"
				  :id="'tabs'+index"
                  >
                    <view :class="[type,activeIndex==index?'active':'']">{{ item.name }}</view>    
                  </view>   
            </scroll-view>
       </view>
</template>

<script>
export default {
    name:'scroll-bar',
	props:{
		  // 主题类型
		  type:{
			   type:String,
			   default:()=>{
				    return 'theme1';
			   }  
		  },
		  // 数据
		  datas:{
			  type:Array,
			  default:()=>{
				   return [];
			  }
		  }
	},
    data(){
         return{
       
            offestLeft:0,
            windowWidth:'',
            domleft:0,
            timer:null,
            activeIndex:0,
         } 
    },
    async mounted(){
           this.windowWidth =  uni.getSystemInfoSync().windowWidth;
        
    },
    methods:{
        // 为了 防止阻塞 使用异步获取dom信息
         async handleClick(index){
              //  防抖--避免用户多次点击
              if(this.timer){
                  clearTimeout(this.timer);
                  this.timer=null;
               }
               this.activeIndex=index;
               this.domleft=0;
               let { getDominfo,windowWidth } = this;
               // 获取dom信息    
               let tabBars = await getDominfo('tabs0');
               let domCenter = (tabBars.width)/2;
               for(let n=0;n<index+1;n++){
                    this.domleft+= tabBars.width; 
               }
                //dom到最左边的距离-domd本身1/2>视口的一半说明可移动小于 
                /**
                 * 
                 * scroll组件当偏移量大于最大限度或者小于最小限度 滚动条会默认不动，不用考虑边界问题
                 * 
                 *  */  
               this.timer = setTimeout(()=>{
                    if(this.domleft+domCenter>windowWidth/2){
                     // 偏移量=dom到最左边的距离-domd本身1/2-视口宽度的一半    
                      this.offestLeft=this.domleft-domCenter-windowWidth/2;
                   }else{
					  this.offestLeft=0
				   }
                   // #ifdef H5
                       this.offestLeft=this.domleft-domCenter-windowWidth/2;
                   // #endif 
                   this.timer=null;
               },200)
                  
         },
		 //  #ifndef H5
         getDominfo(domName){
                 return new Promise((res,inj)=>{
					  uni.createSelectorQuery().in(this).select('#'+domName).boundingClientRect(result => {
					  　　　　if (result) {
					  　　　　　　res(result)
					  　　　　} else {
					  　　　　　　this.getDominfo()
					  　　　　}
					  　　}).exec()
				 })
         },
		 // #endif
		 // #ifndef APP-PLUS || MP-WEIXIN
		 getDominfo(domName){
			     // fields 存在兼容性问题
				 return new Promise((resolve,inject)=>{
				   let doms = uni.createSelectorQuery().select('#'+domName);
				   //   见文档参考 fields 和 exec的 使用方法
				   doms.fields({
						size: true,          // 返回dom节点的大小
						scrollOffset: true,  // 返回节点滚动偏移量
						rect: true           // 是否返回节点布局位置
					}, (data) => {
						resolve(data);
					}).exec();
			 })
		  }
		  // #endif
		
    }
    
}
</script>

<style lang="less" scoped>
 .tabs{
      width: 100%;
      .scrollx{
           width: 100%;
           height: 90upx;
		   white-space: nowrap;
		   padding-top:10upx;
           .tabs-list-item{
                display: inline-block;
                width:150upx;
                height: 50upx;
                text-align: center;
                line-height: 50upx;
				.theme2{
					   font-size: 26upx;
					   display: inline-block;
					   position: relative;
					   width: 80%;
					   text-align: center;
					   position: relative;
					   border-radius: 30upx;
					   border: 1upx solid #F1F1F1;
					   color: #666;
					   &.active{
						  border: 1upx solid #f40; 
						  color: #f40;
					   }
					 
				}
				.theme1{
					   font-size: 28upx;
					   display: inline-block;
					   position: relative;
					   width: 50%;
					   text-align: center;
					   position: relative;
					   &:after{
						content: '';
						width: 0;
						height: 0;
						border-bottom: 4upx solid #f40;
						position: absolute;
						left: 50%;
						bottom: 0;
						transform: translateX(-50%);
						transition: .1s;
					   }
					   &.active{
							font-weight: bold;
						   &:after{
							width: 100%;
						   }
					   }
					 
				}
           }
      }
 }
</style>