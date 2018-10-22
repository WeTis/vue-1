<template>
  <div class="tab">
    <router-link tag="div" to="/rank" class="tab-item">
      <span>Rank</span>
    </router-link>
    <router-link tag="div" to="/recommend" class="tab-item">
      <span>Recommend</span>
    </router-link>
    <router-link tag="div" to="/search" class="tab-item">
      <span>Search</span>
    </router-link>
    <router-link tag="div" to="/Singer" class="tab-item">
      <span>Singer</span>
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'Tab',
  data () {
    return {
      msg: 'hello'
    }
  }
}
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
@import "~common/stylus/variable"

.tab{
  position: fixed;
  top: 50px;
  left: 0;
  display: flex;
  width: 100%;
  height: 50px;
  line-height: 50px;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}
.tab-item{
  flex: 1;
  text-align: center;
}
span{
  display: inline-block;
  height: 40px;
  line-height: 40px;
}
.router-link-active span{
  margin-top: 5px;
  border-bottom: 2px solid $color-theme;
}
</style>