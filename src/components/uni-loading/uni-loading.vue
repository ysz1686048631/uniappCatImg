<template>
<view class="v-spinner" v-show="loading">
    <view class="v-scale v-scale1" v-bind:style="[spinnerDelay1]">
    </view><view class="v-scale v-scale2" v-bind:style="[spinnerDelay2]">
    </view><view class="v-scale v-scale3" v-bind:style="[spinnerDelay3]">
    </view><view class="v-scale v-scale4" v-bind:style="[spinnerDelay4]">
    </view><view class="v-scale v-scale5" v-bind:style="[spinnerDelay5]">
    </view>
  </view>
</template>

<script>
export default {
  
  name: 'ScaleLoader',
  props: {
    loading: {
      type: Boolean,
      default: true
    },
  	color: { 
      type: String,
      default: '#5dc596'
    },
  	height: {
      type: String,
      default: '20px'
    },
  	width: {
      type: String,
      default: '4px'
    },
  	margin: {
      type: String,
      default: '2px'
    },
    radius: {
      type: String,
      default: '2px'
    }
  },
  data () {
    return {
      spinnerStyle: {
      	backgroundColor: this.color,
      	height: this.height,
     		width: this.width,
      	margin: this.margin,
      	borderRadius: this.radius,
        display: 'inline-block',
        animationName: 'v-scaleStretchDelay',
        animationDuration: '1s',
        animationIterationCount: 'infinite',
        animationTimingFunction: 'cubic-bezier(.2,.68,.18,1.08)',
      
      },
      spinnerDelay1: {
        animationDelay: '0.1s'
      },
      spinnerDelay2: {
        animationDelay: '0.2s'
      },
      spinnerDelay3: {
        animationDelay: '0.3s'
      },
      spinnerDelay4: {
        animationDelay: '0.4s'
      },
      spinnerDelay5: {
        animationDelay: '0.5s'
      }
    }
  }
}
</script>

<style>
.v-spinner
{
/*	  font-size: 10px; 
    width: 60px;
    height: 40px;*/
    /*margin: 25px auto;*/
    text-align: center;
}
.v-scale{
	 background-color:#008c8c;
	 height:20px;
	 width: 4px;
	 margin: 2px;
	 display: inline-block;
	 border-radius:3px;
	 animation-name: v-scaleStretchDelay;
	 animation-duration: 1s;
	 animation-iteration-count: infinite;
	 animation-timing-function: cubic-bezier(.2,.68,.18,1.08);
}
@-webkit-keyframes v-scaleStretchDelay
{
    0%
    {
       -webkit-animation-name: inherit;
       -webkit-animation-duration: inherit;
       -webkit-animation-iteration-count: inherit;
       -webkit-animation-direction: inherit;
    }
    100%
    {
        -webkit-transform: scaleY(1);
                transform: scaleY(1);
    }
    50%
    {
        -webkit-transform: scaleY(0.4);
                transform: scaleY(0.4);
    }
}
@keyframes v-scaleStretchDelay
{
    0%
    {
       -webkit-animation-name: inherit;
       -webkit-animation-duration: inherit;
       -webkit-animation-iteration-count: inherit;
       -webkit-animation-direction: inherit;
    }
    100%
    {
        -webkit-transform: scaleY(1);
                transform: scaleY(1);
    }
    50%
    {
        -webkit-transform: scaleY(0.4);
                transform: scaleY(0.4);
    }
}
</style>