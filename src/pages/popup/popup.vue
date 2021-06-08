<!--
 * @Author: your name
 * @Date: 2021-06-08 16:27:15
 * @LastEditTime: 2021-06-08 17:38:30
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \uniss\src\pages\popup\popup.vue
-->
<template>
     <div>
         <button type="default" @tap="showpopofun">点击</button>
		  <unipopup ref="popus" position="left" :styles="{width:'20%'}" v-model="showpopup">
			    <text>asdasd</text>
				<text>asdasd</text>
				<text>asdasd</text>
				<text>asdasd</text>
				<text>asdasd</text>
				<text>asdasd</text>
		  </unipopup>
     </div>
</template>

<script>
import unipopup from '../../components/uni-popup/uni-Drawer.vue'
export default {
    name:'asd',
    components:{ 
        unipopup
    },
    data(){
        return{
             showpopup:true
        }
    },
    methods: {
        // 展示 抽屉  抽屉分为 上 下 左 右四个方向
			showpopofun(){
                // #ifdef H5
                  this.showpopup=true;  // h5端
                // #endif 
                // #ifndef H5   
				  this.$refs.popus.onShowPopus();   //app/小程序端
                // #endif
			}
		}
}
</script>

<style>

</style>