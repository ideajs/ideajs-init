<!-- Created by macmzon@163.com-->
<template>
  <div class="appBarCode">
    <div v-transfer-dom>
      <popup v-model="showBack"></popup>
    </div>
    <appHeader :headerInfo="data.headerInfo"></appHeader>
    <div class="container">
      <div>
        <vue-qr :autoColor="false" :logoMargin="data.logoMargin" :colorDark="data.colorDark" :bgSrc="data.bgSrc" :logoSrc="data.logoSrc" :margin="0" :callback="getCodeInfo" :text="data.codeValue" :logoScale="data.logoScale" :size="data.codeSize"></vue-qr>
      </div>
    </div>
  </div>
</template>

<script>
import VueQr from 'vue-qr'
import {Button} from 'iview'
import { Popup } from 'vux'
import appHeader from'@/components/appConfig/appHeader.vue'
import logoSrc from'@/common/images/small-icon/appBarCode001.png'
import bgSrc from'@/common/images/small-icon/appBarCode014.jpg'

export default {
  name: 'appBarCode',
  data () {
    return {
      showBack: false,
      data: {
        headerInfo: this.$route.meta,
        logoSrc: logoSrc, // 默认二维码中间图片
        bgSrc: bgSrc, // 默认二维码背景图片
        logoScale: 1,
        codeSize: 128, // 二维码宽高
        colorDark: '#0303A0', // 二维码颜色
        logoMargin: 0,
        codeValue: location.href // 扫码后跳转的链接地址
      }
    }
  },
  created () {
      /*自定义顶部header两侧按钮事件+页面左右滑动事件*/
    this.$route.meta.header.leftFuc = this.back                 // header左侧返回按钮事件
    this.$route.meta.touch.rightFuc = this.back                 // 页面向右滑动事件
  },
  methods: {
    back () {
      this.$back({
        path: '/appIndex',
        query: {
          type: '3'
        }
      }, this)
    },
    getCodeInfo (url, id){
//        console.log(url)
    }
  },
  components: {
    VueQr, appHeader, Button, Popup
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">

</style>
