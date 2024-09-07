<template>
  <view class="charts-box">
    <uni-swiper-dot :info="info" :current="current" field="content" :mode="mode">
      <swiper class="swiper-box" @change="change">
        <swiper-item v-for="(item, index) in info" :key="index">
          <view class="swiper-item">
            <!-- <view class="title">十个工业大省规上工业增加值增速</view>
            <view class="pj">
              <view class="dot"></view>
              全国平均水平
            </view> -->
              <Column v-show="index === 0" />
              <Line v-show="index === 1"></Line>
              <ColumnDouble v-show="index === 2"></ColumnDouble>
          </view>
        </swiper-item>
      </swiper>
    </uni-swiper-dot>



  </view>
</template>

<script>
import ColumnDouble from '@/components/ColumnDouble.vue';

export default {
  data() {
    return {
      info: [{
        content: '内容 A'
      }, {
        content: '内容 B'
      }, {
        content: '内容 C'
      }],
      current: 0,
      mode: 'dot',
    };
  },
  onReady() {
    // this.getServerData();
  },
  methods: {
    change(e) {
      this.current = e.detail.current;
    },
  }
};
</script>

<style scoped>
page {
  height: 100%;
}
/* 请根据实际需求修改父元素尺寸，组件自动识别宽高 */
.charts-box {
  width: 100%;
  height: 100%;
 

  /* height: 300px; */
}
.uni-swiper__warp {
  height: 100%;
}
.swiper-box {
  height: 100%;
  position: relative;
}

.swiper-item {
  height: 100%;

}

.title {
  font-size: 18px;
  padding: 10px;
}

.dot {
  width: 15px;
  height: 10px;
  background: #ea7470;
  margin-right: 4px;
}

.pj {
  display: flex;
  align-items: center;
  position: absolute;
  top: 46rpx;
  right: 10rpx;
  font-size: 13px;
  color: #666666;
}
</style>