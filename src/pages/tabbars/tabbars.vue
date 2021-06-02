<!--
 * @Author: your name
 * @Date: 2021-06-02 09:22:41
 * @LastEditTime: 2021-06-02 14:27:17
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \vscdeUniapp\uniss\src\pages\tabbars\tabbats.vue
-->
<template>
       <div>
            <tabbar-temps
             :datas="datas"
			        type="theme1" 
            ></tabbar-temps>
       </div>
</template>

<script>
import tabbarTemps from '../../components/tabbar-temps/tabbar-temps.vue'
export default {
  name:'bars',  
  data(){
     return{
        datas:[
				    {
				       name:'新闻1' 
				    },{
				       name:'新闻2' 
				    },{
				       name:'新闻3' 
				    },{
				       name:'新闻4' 
				    },{
				       name:'新闻5' 
				    },{
				       name:'新闻6' 
				    },{
				       name:'新闻7' 
				    }
				],
     }
  },
  components: { tabbarTemps },

}
</script>

<style>

</style>
