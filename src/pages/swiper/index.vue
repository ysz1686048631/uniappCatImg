<!--
 * @Author: your name
 * @Date: 2021-06-01 17:43:17
 * @LastEditTime: 2021-06-01 18:11:24
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vscdeUniapp\uniss\src\pages\swiper\index.vue
-->
<template>
     <div>
         <swiperTemp
          @handle-tap="handleclick"
          :list="list"
           interval="1500"
          dotActiveColor="#007fff"
         />
     </div>
</template>

<script>
import swiperTemp from '../../components/swiper-temps/swiper-temps'
export default {
     name:'asdsa',
     components:{
          swiperTemp
     },
     data(){
         return {
              list:[
						 {
							 img:"../../static/t1.png",
							 url:'1'
						 },{
							 img:"../../static/t2.png",
							  url:'2'
						 },{
							 img:"../../static/t3.png",
							  url:'3'
						 },{
							 img:"../../static/t5.png",
							  url:'4'
						 }
					],
         }
     },
   
     methods:{
          handleclick(e){
               console.log(e)
          }
     }
}
</script>

<style>

</style>