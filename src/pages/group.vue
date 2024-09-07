<template>
  <view class="bg-[#1e94eb] p-1 h-fill">
    <view class="flex justify-between">
      <view class="bg-white flex-1 rounded-md h-37" >
        <Column v-if="currentLeft === 'Column'" :enable-scroll="true" :ontouch="true" :showIcon="true" @openSheet="openSheet"></Column>
        <ColumnDouble v-else :enable-scroll="true" :ontouch="true" :showIcon="true" @openSheet="openSheet"></ColumnDouble>
      </view>
      <view class="bg-white flex-1 rounded-md ml-1 h-37">
        <Line v-if="currentRight === 'Line'" :enable-scroll="true" :ontouch="true" :showIcon="true" @openSheet="openSheet"></Line>
        <ColumnDouble v-else :enable-scroll="true" :ontouch="true" :showIcon="true" @openSheet="openSheet"></ColumnDouble>
      </view>
    </view>
    <view class="bg-white mt-1 rounded-md h-37">
      <ColumnDouble v-if="currentBottom === 'ColumnDouble'" :showIcon="true" @openSheet="openSheet"></ColumnDouble>
      <Column v-if="currentBottom === 'Column'" :showIcon="true" @openSheet="openSheet"></Column>
      <Line v-if="currentBottom === 'Line'" :showIcon="true" @openSheet="openSheet"></Line>
    </view>
  </view>
</template>

<script>
import JsBridge from '@/utils/index.js';

export default {
  data() {
    return {
      comList: ['Column', 'Line', 'ColumnDouble'],
      currentBottom: 'ColumnDouble',
      currentRight: 'Line',
      currentLeft: 'Column'
    }
  },
  mounted(){
  	// 监听app触发monitorTestData，进行监听接收数据
    JsBridge.registerHandler('monitorTestData', (data) => {
        console.log("监听到的1数1据",data)
        this.monitor= data;
    })
  },
  methods: {
    openSheet(type) {
      console.log('eee', type);
      
    },
    getData() {
      JsBridge.callHandler('getAppData',{'param': "你好，这是我JS传递给你的数据"}, (data) => {
         console.log("获取到的数据",data)
          this.contnet = data;
      })
    }
  }
}
</script>

<style>

</style>