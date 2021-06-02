<!--
 * @Author: your name
 * @Date: 2021-06-01 17:43:17
 * @LastEditTime: 2021-06-01 18:09:32
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vscdeUniapp\uniss\src\pages\swiper\index.vue
-->
<template>
     <div>
         <gridTemp
          colmns="4"
          :dataList="grid"
          @handle-tap="onclicktap"
          :round="false"
         />
     </div>
</template>

<script>
import gridTemp from '../../components/grid-temps/grid-temps'
export default {
     name:'grid',
     data(){
         return {
           grid:[
					 {
						  img:'../../static/zhuti.svg',
						  name:'主体导航',
						  url:'asd'
					 },
					 {
						  img:'../../static/zhuti.svg',
						  name:'区域导航',
						  url:'asd'
					 },
					 {
						  img:'../../static/zhuti.svg',
						  name:'招商地图',
						  url:'asd'
					 },{
						  img:'../../static/zhuti.svg',
						  name:'招商地图',
						  url:'asd'
					 }
					
				]
         }
     },
     components:{
          gridTemp
     },
     methods:{
          onclicktap(e){
               console.log(e)
          }
     }
}
</script>

<style>

</style>