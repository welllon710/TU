<template>
  <view style="height: 100%;">
    <view class="title">
      <view>重点行业规上工业增加值增速</view>
      <uni-icons v-if="showIcon" type="more-filled" size="20" @click="$emit('openSheet', 'ColumnDouble')"></uni-icons>
    </view>
    <view class="charts-q">
      <qiun-data-charts type="column" :opts="opts" :chartData="chartData" tooltipFormat="tooltipDemo1"
        @getIndex="getIndex" :ontouch="ontouch" />
    </view>
  </view>
</template>

<script>
export default {
  props: {
    enableScroll: {
      type: Boolean,
      default: false,
    },
    ontouch: {
      type: Boolean,
      default: false,
    },
    showIcon: {
      type: Boolean,
      default: false,
    }
  },
  data() {
    return {
      chartData: {},
      //您可以通过修改 config-ucharts.js 文件中下标为 ['column'] 的节点来配置全局默认参数，如都是默认参数，此处可以不传 opts 。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
      opts: {
        // enableMarkLine: true,
        dataLabel: true,
        enableScroll: this.enableScroll,
        title: {
          name: '1111111111111'
        },
        color: ["#5ba9eb", "#e8ae6b", "#FAC858", "#EE6666", "#73C0DE", "#3CA272", "#FC8452", "#9A60B4", "#ea7ccc"],
        padding: [0, 15, 25, 15],
        legend: {
          position: 'top',
          float: 'right',
          offsetX: 0,
        },
        xAxis: {
          disableGrid: true,
          boundaryGap: "center",
          scrollShow: true,
          itemCount: 4
        },
        yAxis: {
          showTitle: false,
          splitNumber: 4,
          data: [
            {
              titleOffsetY: -10,
              title: '单位 /%',
              min: -40,
              max: 40
            }
          ]
        },
        extra: {
          column: {
            type: "group",
            width: 30,
            activeBgColor: "#000000",
            activeBgOpacity: 0.08,
            seriesGap: 2,
            categoryGap: 3,
            barBorderCircle: false,
            linearType: "opacity",
            linearOpacity: 0.7,
            // customColor: [
            //   '#5793df', '#78b1f2'
            // ],
            colorStop: 0.1,
            meterBorder: 1,
            meterFillColor: "#FFFFFF",
            labelPosition: "top"
          },
        }
      }
    };
  },
  mounted() {
    this.getServerData();
  },
  methods: {
    change(e) {
      this.current = e.detail.current;
    },
    getIndex(e) {
      // console.log(e)
      // this.opts.enableMarkLine = !this.opts.enableMarkLine
    },
    getServerData() {
      //模拟从服务器获取数据时的延时
      setTimeout(() => {
        //模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
        let res = {
          categories: ["2018", "2019", "2020", "2021", "2022", "2023", "2018", "2019", "2020", "2020"],
          series: [
            {
              name: "2024年5月",
              data: [20, -20, 25, -25, 30, -30]
            },
            {
              name: "2024年6月",
              data: [20, -20, 25, -25, 30, -30]
            }
          ]
        };
        this.chartData = JSON.parse(JSON.stringify(res));
      }, 500);
    },
  }
};
</script>

<style scoped>
.charts-q {
  height: calc(100% - 20rpx - 10rpx);
}

.title {
  font-size: 16px;
  padding: 10rpx 10rpx 0 10rpx;
  display: flex;
  align-items: center;
  justify-content: space-between;
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