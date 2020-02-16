<template>
  <div>
    <div class="nav_wrap">
      <div class="wrap" ref="wrap" @scroll="scroll($event)">
        <ul class="view" ref="view" >
          <li v-for="(item,index) in 100" :key="index">{{index}}</li>
        </ul>
      </div>
      <div class="track" ref="track">
        <div class="thumb" ref="thumb"></div>
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
    console.log(wrapHeight,viewHeight,trackHeight,thumbHeight)
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
       console.log(wrapClientHeight,wrapScrollTop)
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
    margin: 20px auto;
    position: relative;
  }
  .wrap{
    height: 100%;
    width: 220px;
    overflow-y: auto;
    overflow-x: hidden;
  }
  .track{
    position: absolute;
    right: 0px;
    top: 0;
    width: 10px;
    height: 100%;
    border: 1px solid grey;
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
