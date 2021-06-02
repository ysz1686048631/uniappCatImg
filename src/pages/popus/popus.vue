<!--
 * @Author: your name
 * @Date: 2021-04-30 15:21:49
 * @LastEditTime: 2021-06-01 17:45:07
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vscdeUniapp\uniss\src\pages\popus\popus.vue
-->
<template>
      <view class="PopusDome">
          <button @tap="onshowpop"> 展开</button>
            <popustemp 
            :showpopus="showpopus"
            type="top"
            @handleClick="handleClick"
            :cancelshow="false"
            />
      </view>
</template>

<script>
import popustemp from '@/components/popu-temps/popustemp.vue'
export default {
    name:'popus',
    data(){
         return{
              showpopus:false,
         }
    },
    components:{
         popustemp
    },
    methods:{
         onshowpop(){
               this.showpopus = true
         },
         handleClick(e){
             this.showpopus = false;
         }
    }
}
</script>

<style lang="less" scoped>
     .PopusDome{
         
     }
</style>