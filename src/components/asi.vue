/**
*  Class: asi
*  Author: Niu Xiaoyu
*  Date: 16/7/2.
*  Description: 在备选列表中随机选择一项
*/
<script>
  import { reAsiAction } from '../vuex/actions';
  import { getSelected } from '../vuex/getters';
  export default {
    data() {
      return {
        siteInfo: {
          sitename: "去吃啥？"
        }
      }
    },
    computed: {

    },
    methods: {
      goBack: function (e) {
        history.go(-1);
      },

    },
    vuex: {
      actions: {
        reAsi: reAsiAction
      },
      getters: {
        // 注意在这里你需要 `getSelected` 函数本身而不是它的执行结果 'getSelected()'
        selectedValue: getSelected
      }
    },
    route: {
      data: function (transition) {
        var me = this;
        setTimeout(function () {
          me.reAsi();
          transition.next();
        }, 1000)
      }
    }
  }
</script>
<template>
  <header class="header mui-bar mui-bar-nav">
    <a @click="goBack" class="mui-icon mui-icon-left-nav mui-pull-left"></a>
    <h1 id="title" class="mui-title">{{siteInfo.sitename}}</h1></header>
  <div class="mui-content asi-page">
    <div class="loading" v-if="$loadingRouteData">
      <div class="spinner">
        <div class="double-bounce1"></div>
        <div class="double-bounce2"></div>
      </div>
      <span>给我一点时间...</span>
    </div>
    <div v-if="!$loadingRouteData" class="asi-box">
      <div class="asi-card" :class="selectedValue.img">
        <div class="asi-card-title" style="background-color:rgba(173, 171, 163, 0.7);">
          <span>{{selectedValue.title}}</span></div>
      </div>
      <div class="re-asi-btn" @click="reAsi"><span>不对不对，再选一次！</span></div>
    </div>
  </div>
</template>
