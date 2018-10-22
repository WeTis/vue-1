<template>
  <div id="app">
   <Head></Head>
   <tab></tab>
   <router-view></router-view>
  </div>
</template>

<script>
import Head from 'components/Head'
import Tab from 'components/tab/tab'
export default {
  name: 'App',
  components: {
    Head,
    Tab
  }
}
</script>

<style>
#app{
  margin-top: 100px;
}

body,div,span,p,ul,li{
  padding: 0;
  margin: 0;
}
ul,li{
  list-style-type: none;
}
</style>
