<template>
  <div @mousemove="thumbMove" @mouseup="thumbOut">
    <div class="nav_wrap">
      <div class="wrap" ref="wrap" @scroll="scroll($event)">
        <ul class="view" ref="view" >
          <li v-for="(item,index) in 100" :key="index">{{index}}</li>
        </ul>
      </div>
      <div class="track" ref="track" @mousedown="trackDown">
        <div class="thumb" ref="thumb" @mousedown.stop="thumbDown"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'vitural-scroll',
  mounted() {
    const wrapHeight = this.$refs.wrap.clientHeight
    const viewHeight = this.$refs.view.clientHeight
    const percent = wrapHeight/viewHeight
    const trackHeight = this.$refs.track.clientHeight
    this.$refs.thumb.style.height = percent*trackHeight+'px'
    const thumbHeight = this.$refs.thumb.clientHeight
  },
  data() {
    return {
    
    }
  },
  methods: {
     scroll(event) {
       const wrapClientHeight = this.$refs.wrap.clientHeight
       const wrapScrollTop = this.$refs.wrap.scrollTop
       this.moveY = wrapScrollTop*100/wrapClientHeight
       this.$refs.thumb.style.transform=`translateY(${this.moveY}%)`
     },
     thumbDown(e) {
       console.log(e)
       this.start = true
       this.startY = e.clientY
     },
     thumbMove(e) {
       if(!this.start) return
        console.log(e)
       const thumb = this.$refs.thumb
       const thumbRect = thumb.getBoundingClientRect()
       
       const moveY = e.clientY-this.startY>0?e.clientY-this.startY:this.startY-e.clientY
       const thumbMoveYPercent = moveY*100/thumbRect.height
       console.log( thumbMoveYPercent)
       thumb.style.transform = `translateY(${thumbMoveYPercent}%)`
     },
     thumbOut(e) {
       console.log('停止',e)
       this.start = false
       this.startY = 0
     },
     trackDown(e) {
       console.log(e)
       const thumb = this.$refs.thumb
       const view = this.$refs.view
       const track = this.$refs.track
       const wrap = this.$refs.wrap
       const thumbRect = thumb.getBoundingClientRect()
       const trackRect = track.getBoundingClientRect()
       const wrapRect = wrap.getBoundingClientRect()
       let thumbMoveY
       if(e.clientY<thumbRect.y-trackRect.y)       //thumb相对父级顶部的距离比鼠标点击位置距离父级顶部距离大
        thumbMoveY = e.clientY-trackRect.y
       else
        thumbMoveY = e.offsetY-thumbRect.height
       
       const thumbMoveYPercent = thumbMoveY/thumbRect.height
       thumb.style.transform = `translateY(${thumbMoveYPercent*100}%)`    //移动小方块
       view.style.transform = `translateY(${-thumbMoveYPercent*wrapRect.height}px)`    //移动视图
     }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .nav_wrap{
    height: 400px;
    width: 200px;
    overflow: hidden;
    border: 1px solid #ccc;
    margin: 0px auto;
    position: relative;
  }
  .wrap{
    height: 100%;
    width: 220px;
    overflow-y: auto;
    overflow-x: hidden;
  }
  .view {
  }
  .track{
    position: absolute;
    right: 0px;
    top: 0;
    width: 10px;
    height: 100%;
    border-left: 1px solid #ccc;
  }
  .thumb{
    position: absolute;
    right: 0px;
    height: 100%;
    top: 0;
    width: 10px;
    background-color: grey;
  }
</style>
