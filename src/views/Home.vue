<template>
  <div class="home">
    home
    <!-- <div v-customDirective>自定义指令</div> -->
    <button @click="unbindHandler">点击解绑</button>
    <div :class="red | changeBlue">{{red}}</div>
  </div>
</template>

<script>
// filters可以用在两个地方
// 一个是moustouch语法糖
// 一个是动态的class
// 过滤器还可以串联，因为过滤器本身是一个函数
export default {
  name: 'Home',
  components: {
  },
  data(){
    return {
      flag: true,
      red: 'red',
      blue: 'blue'
    }
  },
  filters:{
    changeBlue(val) {
      if(val == 'red') {
        return val = 'blue'
      }
    }
  },
  // 组件内独享守卫,进入路由之前，不能获取组件的实例
  beforeRouteEnter(to,from,next){
    console.log("to===",to)
    console.log("from===",from)
    console.log("this===",this)
    next(vm=>{
      // 这个vm就是组件的实例
       console.log("vm===",vm)
    })
  },
  beforeRouteUpdate() {
    console.log("路由离开的时候")
  },
  methods:{
    unbindHandler() {
      this.$destroy()
      let str = 'Hello world'
      let lowerStr = str.toLowerCase()
      console.log("lowerStr",lowerStr)
    }
  }
}
</script>
<style scoped>
 .red {
  color: red;
 }
 .blue {
  color: blue
 }
</style>