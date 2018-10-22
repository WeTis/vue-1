<template>
  <div class="head">
     网易云音乐
  </div>
</template>

<script>
export default {
  name: 'Head',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
@import "~common/stylus/variable"

.head{
  position: fixed;
  height: 50px;
  line-height: 50px;
  text-align: center;
  background-color: $color-background;
  color: #fff;
  width: 100%;
  left: 0;
  top: 0;
}
</style>