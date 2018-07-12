<template>  
    <div v-if="promptShow"  :class="{'show-prompt-tran':promptShow} ">
       <div class="prompt-bg"></div>
        <div class="prompt-warp" >
            <div class="prompt-title" :html="promptTitle">{{promptTitle}}</div>
            <div class="prompt-content">               
                <aside :html="content">
                   {{content}}
                   <slot></slot>
                </aside>
            </div>
            <div class="prompt-button">
              <span class="sure" @click="sureFun" :html="sure">{{sure}}</span>
              <span class="cancle rightborder" @click="cancleFun " v-if='confirm' :html="cancle">{{cancle}}</span>
            </div>
        </div>
    </div>
</template>
<script>
/*
* 提示窗功能，支持alert/confimr
* @param [String] promptTitle 
*/
export default {
  name: 'prompt',
  props: {
    //提示框头部
    promptTitle: {
      type: String,
      default: '提示'
    },
    //确认按钮文字
    sure: {
      type: String,
      default: '确认'
    },
    // 提示内容
    content: {
      type: String,
      default: '哎呀，报错了唉，等一会吧！'     
    },
    // 取消按钮文字 
    cancle: {
      type: String,
      default: '取消'
    },
    // 是否开起comfirm
    confirm: {
      type: Boolean,
      default: false
    },
    // 控制弹出显示隐藏
    promptShow:{
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      // 存组件内部变量，监听是否显示
      showValue: false 
    };
  },
  // 初始化
  created () {
    if (typeof this.promptShow !== 'undefined') {
      this.showValue = this.promptShow;
    }
  },
  methods: {
    // 点确认方法
    sureFun () {
      this.showValue = false;   
      this.$emit('on-sure', true);
    },
    // 取消方法
    cancleFun () {  
       this.showValue = false;
       this.$emit('on-cancle', false);
    }
  },
  // 事件监听
  watch: {
    promptShow (val) {
      this.showValue = val;
    }, 
    showValue (val) { 
      this.promptShow = val;
      this.$emit('input', val);
    }
  }
};
</script>
<style>   
  .padl-30 {
		padding-left: 20px;
	}
	.prompt-bg {
		z-index: 10;
		position: fixed;
		top:0;
		left:0;
		right:0;
		left:0;
		bottom:0;
		background: rgba(0,0,0,0.5);
	}
	.prompt-warp {
		font-size:12px;
		border:1px solid #ccc;	
		z-index: 15;
		position:absolute;
		text-align:center;
		top:50%;
		left:50%;
		background:#FFFFFF;
		width:80%;
		min-height:150px;
		border-radius: 10px;
		transform:translate(-50%,-50%);
	}
	.prompt-title{
		color: #222;
		font-size: 18px;
		line-height: 50px;
		min-height: 50px;
  }
	.prompt-content{
    position: relative;
		text-align:left;
		word-wrap: break-word;
		padding:10px 15px;
    max-height:300px;
    overflow: hidden; 
		min-height:60px;
  }
  .prompt-content aside{
    overflow-y:scroll;
    max-height:300px; 
    word-wrap: break-word;
  }
	.prompt-button{
		border-top:1px solid #C8C8CD;
		display:flex;
		align-items: center;
    text-align: center;
    width:100%;
  }
  .prompt-button span{
      color:#f00;
			flex:1;
			display:inline-block;
			line-height:50px;	
  }
	.prompt-button > span.rightborder{
    color:#000;
		border-left:1px solid #C8C8CD;
	}
	.prompt-button {
		line-height:50px;
		border-top:1px solid #C8C8CD;
	}
</style>