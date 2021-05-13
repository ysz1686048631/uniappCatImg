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
import popustemp from '@/components/poputemp/popustemp.vue'
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