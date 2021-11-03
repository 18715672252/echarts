<template>
    <div class="maps" ref="mapContent">

    </div>
</template>

<script>
import MapData from '../utils/MapData'
export default {
  name: 'maps',
  data () {
    return {
      options: {
        tooltip: {
          trigger: 'item'
        },
        series: [
          {
            name: '上海市刑事案件分布图',
            type: 'map',
            top: '10%',
            mapType: 'SH', // 自定义扩展图表类型
            scaleLimit: {
              min: 1
            },
            label: {
              show: true,
              offset: [20, 0],
              color: '#42526E'
            },
            layoutCenter: ['50%', '50%'],
            // 如果宽高比大于 1 则宽度为 100，如果小于 1 则高度为 100，保证了不超过 100x100 的区域
            layoutSize: 500,
            itemStyle: {
              areaColor: '#E1ECFD'
            },
            emphasis: {
              areaColor: 'red',
              label: {
                color: '#fff'
              },
              itemStyle: {
                areaColor: '#2F6BFF'
              }
            }
          }
        ]
      }
    }
  },
  mounted () {
    const myChart = this.$echarts.init(this.$refs.mapContent)
    this.$echarts.registerMap('SH', MapData)
    myChart.setOption(this.options)
    myChart.dispatchAction({
      type: 'highlight', // 高亮指定的数据图形。通过seriesName或者seriesIndex指定系列。如果要再指定某个数据可以再指定dataIndex或者name。
      name: '青浦区'
    })
    // this.chartInstance.dispatchAction({
    //   type: 'downplay', // 取消高亮指定的数据图形
    //   seriesIndex: 0
    // })
    myChart.on('click', params => {
      console.log(params)
    })
  }
}

</script>

<style scoped>
.maps {
    width: 100%;
    height: 100%;
}
</style>
