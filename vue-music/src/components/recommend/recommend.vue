<template>
  <div id="recommend">
    <ul :style="{width: this.ulWidth + 'px', transform: 'translateX(-' + this.clientwidth + 'px)'}">
      <li v-for="(item,index) in dots" v-bind:key="index" :style="{width:width+'px'}"><a :href="item.linkUrl"><img :src="item.picUrl"></a></li>
    </ul>
    <div class="dotlist">
      <span v-for="(item,index) in dotlist" v-bind:key="index" class="dots" v-on:click="_clickDots(index)"></span>
    </div>
  </div>
</template>

<script>
import {getRecommend} from 'api/recommend'
import {ERR_OK} from 'api/config'

export default {
  name: 'Recommend',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      dots: [],
      dotlist: [],
      clientwidth: 0,
      ulWidth: 0,
      width: 0,
      indexL: 0,
      ulStyle: { }
    }
  },
  created() {
    this._getRecommend()
  },
  methods: {
    _getRecommend() {
      getRecommend().then((res) => {
        if (res.code === ERR_OK) {
          this.dotlist.push(...res.data.slider)
          this.dots.push(res.data.slider[res.data.slider.length - 1])
          this.dots.push(...res.data.slider)
          this.dots.push(res.data.slider[0])
          this.clientwidth = document.documentElement.clientWidth
          this.ulWidth = document.documentElement.clientWidth * this.dots.length
          this.width = document.documentElement.clientWidth
          this.repeatMove(4000)
          console.log(this.clientwidth)
        }
      })
    },
    _clickDots(Index) {
      // 获取当前的位置
      console.log(Index)
    },
    repeatMove(repeat, fn) {
      // var timmm = null
      setInterval(() => {
        // clearInterval(timmm)
        this.moveImg()
        fn && fn()
      }, repeat)
    },
    moveImg() {
      this.moveAlang(50, (speedWidth) => {
        this.clientwidth += speedWidth
      }, (w) => {
        console.log(w)
        if (this.clientwidth === 6 * document.documentElement.clientWidth) {
          this.clientwidth = document.documentElement.clientWidth
        } else if (this.clientwidth === 0) {
          this.clientwidth = 5 * document.documentElement.clientWidth
        }
      })
    },
    compterSpeedArr(width, alltime, time) {
      var timeLength = alltime / time
      var m = 0
      for (var i = 1; i <= timeLength; i++) {
        m += i * i
      }
      var x = width / m
      var y = (x).toFixed(2) * 1
      var arr = []
      var aAll = 0
      for (var v = 1; v <= timeLength; v++) {
        var ar = Math.ceil(y * v * v)
        aAll += ar
        if (aAll <= width) {
          arr.push(ar)
        } else {
          break
        }
      }
      var mmm = 0
      for (var d = 0; d < arr.length; d++) {
        mmm += arr[d]
      }
      var xcc = width - mmm
      console.log(xcc)
      var indexx = 0
      for (var j = arr.length - 1; j >= 0; j--) {
        if (j > 0) {
          if (xcc <= arr[j] && xcc > arr[j - 1]) {
            indexx = j
            arr.splice(indexx, 0, xcc)
            break
          } else if (xcc >= arr[j]) {
            indexx = j + 1
            arr.splice(indexx, 0, xcc)
            break
          }
        } else {
          indexx = 0
          arr.splice(indexx, 0, xcc)
        }
      }
      return arr
    },
    moveAlang(repeat, fn, endFn, preNext) {
      if (!preNext) {
        preNext = 1// 下一页 2 上一页
      }
      var arr = this.compterSpeedArr(document.documentElement.clientWidth, 1000, 50)
      console.log(arr)
      var moveWidth = 0
      var index = arr.length - 1
      var timer = null
      timer = setInterval(function() {
        if (preNext === 1) {
          moveWidth += arr[index]
        } else if (preNext === 2) {
          moveWidth -= arr[index]
        }
        if (index < 0) {
          endFn && endFn(moveWidth)
          clearInterval(timer)
        } else {
          // console.log(moveWidth)
          // console.log(arr[index])
          fn && fn(arr[index])
          index = index - 1
        }
      }, repeat)
    }
  }
}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
#recommend{
  width: 100%;
  overflow: hidden;
}
ul,li{
  width: 100%;
  font-size: 0;
}
li{
  display: inline-block;
}
li img{
  width: 100%;
}
.dots{
  display: inline-block;
  margin: 0 10px;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: red;
}
#recommend{
  position: relative;
}
.dotlist{
  position: absolute;
  bottom: 10px;
  left: 50%;
  width: 150px;
  margin-left: -75px;
}
</style>