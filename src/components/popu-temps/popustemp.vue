<template>
      <view :class="[
         'Popustemp',
         showpopus?'active':''
      ]">
                <view :class="[
                     'Popustemp-alert',
                      type,
                      showpopus && type=='top'?'activetop':'',
                      showpopus && type=='scale'?'activescale':''
                   ]">
                    <view class="Popustemp-alert_title">
                         提示
                    </view>
                    <view class="Popustemp-alert_text">
                         确定要退出吗
                    </view>
                    <view class="Popustemp-alert_bar">
                        <view v-if="cancelshow" @tap="onCancel">取消</view>
                        <view @tap="onDeter">确定</view>  
                    </view>   
                </view>     
      </view>
</template>

<script>
export default {
    name:'popus',
    props:{
         showpopus:{
              default:function(){
                   return false;
              }
         },
         type:{
              default:function(){
                  return 'top'
              }
         },
         cancelshow:{
              default:function(){
                   return true;
              }
         }
    },
    methods:{
         onCancel(){
            this.$emit('handleClick',0)
         },
         onDeter(){
            this.$emit('handleClick',1) 
         }
    }
}
</script>

<style lang="less" scoped>
     .fontstyle(@color,@size,@weight){
          color: @color;
          font-size: @size;
          font-weight: @weight;
     }
     .disflex(@type){
         display: flex;
         flex-direction: @type;
     }
     .Popustemp{
            position:fixed;  
            width: 100%;
            height: 100vh;
            left: 0;
            top: 0;
            background: rgba(199, 198, 198, 0.671);
            .disflex(column);  
            align-items: center;
            justify-content: center;
            z-index: -999;
            visibility: hidden;
            opacity: 0;
            transition:all .1s ease-in 0s;
            &.active{
                z-index: 999;
                visibility:visible;
                opacity: 1;  
            }
            &-alert{
                  width:60%;  
                 .disflex(column);
                 background: floralwhite;
                 border-radius: 10upx;
                 overflow: hidden;
                 &.top{
                      transform: translateY(-800upx);
                      transition:all .2s cubic-bezier(0, 1.46, 0.36, 0.94) 0s;
                 }
                 &.scale{
                      transform: scale(.2);
                      transition:all .2s cubic-bezier(0, 1.46, 0.36, 0.94) 0s;
                 }
                 &.activescale{
                      transform: scale(1);
                 }
                 &.activetop{
                    transform: translateY(-10upx);  
                 }
                 &_title{
                      .fontstyle(#393e4d, 32upx, bold);
                       text-align: center;
                       margin-top: 20upx;
                 }
                 &_text{
                      .fontstyle(#393e4d, 28upx, 100);
                      text-align: center;
                      padding: 20upx 0;
                 }
                 &_bar{
                      border-top: 1px solid #f1f1f1;
                      .disflex(row);
                      &>view{
                           flex: 1;
                           .fontstyle(#393e4d, 26upx, 100);
                           text-align: center;
                           padding: 20upx 0;
                           &:nth-of-type(1){
                                border-right: 1px solid #f1f1f1;
                           }

                      }

                 }
            }
     }
</style>