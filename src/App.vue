<template>
  <div id="q-app">
    <router-view />
    <custom-cursor
    v-if="$q.platform.is.desktop"
    :targets="['img', 'a', 'button', 'i', 'svg']"
    :circleColor="'#00867a'"
    :circleColorHover="'#fff'"
    :dotColor="'#ed3833'"
    :dotColorHover="'#5dc855'"
    :hoverSize="1.8"
  ></custom-cursor>
  </div>
</template>
<script>
import Vue from 'vue'
import CustomCursor from 'components/CustomCursor'
import routes from './router/routes'

Vue.prototype.windowObj = window
const throttle = (callback, limit) => {
    var waiting = false;                      // Initially, we're not waiting
    return function () {                      // We return a throttled function
        if (!waiting) {                       // If we're not waiting
            callback.apply(this, arguments);  // Execute users function
            waiting = true;                   // Prevent future invocations
            setTimeout(function () {          // After a period of time
                waiting = false;              // And allow future invocations
            }, limit);
        }
    }
}
export default {
  name: 'App',
  components: {
    CustomCursor
  },
  // mounted: function () {
  //   window.addEventListener("mousewheel", throttle((ev) => {
  //     if ((window.innerHeight + window.scrollY) >= (document.body.offsetHeight - 1 )) {
  //       const pages = routes[0].children
  //       const curr = this.$router.currentRoute.path
  //       const currIndex = pages.findIndex((elm) => {
  //         return elm.path === curr || (curr === '/' && elm.path === '')
  //       })
  //       const nextPath = pages[(currIndex+1)%6].path
  //       console.log(curr, currIndex, nextPath)
  //       this.$router.push({ path: nextPath })
  //     }
  //   }, 200), false)
  // }
}
</script>
<style>
#q-app { cursor: none }
aside { cursor: auto }
</style>