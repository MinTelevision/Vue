<template>
  <div id="app">
    <div class="xl" :style="{'height':h+'px'}">{{name}}</div>
    <div class="list" @touchstart="scrollStart($event)" @touchmove="scrollMove($event)" @touchend="scrollEnd($event)"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      name:'加载中',
      h:0,
      scrollY:0,
    }
  },
  methods: {
    scrollStart(e){
      this.scrollY=e.targetTouches[0].pageY
    },
    scrollMove(e){
      // 移动的时候
      if(window.scrollY==0){
        this.h=e.targetTouches[0].pageY-this.scrollY
        if(this.h>=100){
          this.h=100;
        }
      }else{
        return;
      }
    },
    scrollEnd(e){
      if(this.h<100){
        this.h=0;
      }else if(this.h==100){
        setTimeout(()=>{
          this.h=0;
        },500)
      }
    }
  },
}
</script>
<style lang="scss" scoped>
#app{
  .xl{
    background-color:blue;
    text-align:center;
    color:#fff;
    overflow:hidden;
  }
  .list{
    height:1000px;
    background: #e4393c;
  }
}
</style>


