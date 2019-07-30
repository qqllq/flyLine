//vue实现飞线图，下面是index.vue
//需要引入echarts amap echarts-amap，可以在index.html页面引入也可以在main.js引入npm
<template>
  <div class="content-box">
    <!-- 设置ref方便获取到当前元素 -->
    <!-- echart容器div必须设置高度，否则不显示 -->
    <div ref="echart" style="height:745px;"></div>
  </div>
</template>
<script>
const series_ = [
  // 两点之间的特效线
  {
    name: 'your name',
    coordinateSystem: 'amap',
    type: 'lines',
    zlevel: 1,
    effect: {
      show: true,
      period: 2,
      trailLength: 0.7,
      color: '#2267f7',
      symbolSize: 3
    },
    lineStyle: {
      normal: {
        color: '#2267f7',
        width: 0,
        curveness: 0.2
      }
    },
    data: [
      {
        fromName: 'from city',
        toName: 'to city',
        coords: [[from,city], [to, city]],//设置经纬度
        value: 95
      }//如果有多条线可以在data里增加
    ]
  },
  // 两点之间的连线
  {
    name: 'message',
    coordinateSystem: 'amap',
    type: 'lines',
    zlevel: 2,
    symbol: ['none', 'arrow'],
    symbolSize: 10,
    lineStyle: {
      normal: {
        color: '#6ecef2',
        width: 1,
        opacity: 0.6,
        curveness: 0.2
      }
    },
    data: [
      {
        fromName: 'from city',
        toName: 'to city',
        coords: [[from,city], [to, city]],//设置经纬度
        value: 95
      }//如果有多条线可以在data里增加
    ]
  },

  // 圆点
  {
    name: '圆点',
    type: 'effectScatter',
    coordinateSystem: 'amap',
    zlevel: 2,
    symbolSize: 20,
    rippleEffect: {
      brushType: 'stroke'
    },
    label: {
      normal: {
        show: true,
        position: 'bottom',
        formatter: '{b}'
      }
    },
    itemStyle: {
      normal: {
        color: '#4c61c8'
      }
    },
    data: [
      {
        name: 'your name',
        value: [, , 95]空位设置经纬度
      }//如果有多个圆点也可以在data里增加
    ]
  }
];
export default {
  mounted() {
    this.$nextTick(() => {
      this.initEchart();
    });
  },
  methods: {
    initEchart() {
      // 获取DOM节点并初始化
      let chart = this.$echarts.init(this.$refs.echart);
      // 编写echart参数
      let option = {
        amap: {
          zoom: 10,
          zooms: [3, 20],
          mapStyle: 'amap://styles/darkblue', // 地图主题
          center: [110, 33], // 中心点
          lang: 'en',
          resizeEnable: true
        },
        animation: false,
        series: series_,
        tooltip: { return: '' }//可以设置tooltip
      };
      // 设置图表的参数
      chart.setOption(option);
    }
  }
};
</script>
