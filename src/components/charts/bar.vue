<template>
  <div ref="dom" class="charts chart-bar"></div>
</template>

<script>
import echarts from 'echarts'
import tdTheme from './theme.json'
import { on, off } from '@/libs/tools'
echarts.registerTheme('tdTheme', tdTheme)
export default {
  name: 'ChartBar',
  props: {
    value: Object,
    text: String,
    subtext: String
  },
  data () {
    return {
      dom: null
    }
  },
  methods: {
    resize () {
      this.dom.resize()
    }
  },
  mounted () {
    let lineOption = {
      lineStyle: {
        color: 'rgba(151,151,151,0.5)'
      }
    }
    let fontColor = '#666'
    this.$nextTick(() => {
      let xAxisData = Object.keys(this.value)
      let seriesData = Object.values(this.value)
      let option = {
        title: {
          text: this.text,
          subtext: this.subtext,
          x: 'left',
          textStyle: {
            fontSize: '12px',
            color: '#333'
          }
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        xAxis: [{
          type: 'category',
          data: xAxisData,
          axisLine: {
            lineStyle: {
              color: 'rgba(151,151,151,0)',
              type: 'dashed'
            }
          },
          splitLine: {
            lineStyle: {
              color: 'rgba(151,151,151,0)',
              type: 'dashed'
            }
          },
          axisTick: {
            show: false
          },
          axisLabel: {
            margin: 10,
            color: fontColor,
            textStyle: {
              fontSize: 14
            }
          }
        }],
        yAxis: [{
          axisLabel: {
            formatter: '{value}',
            color: fontColor
          },
          axisTick: {
            show: false
          },
          axisLine: lineOption,
          splitLine: lineOption
        }],
        series: [{
          data: seriesData,
          barWidth: '20px',
          type: 'bar',
          itemStyle: {
            normal: {
              color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                offset: 0,
                color: '#00BD89' // 0% 处的颜色
              }, {
                offset: 1,
                color: '#C9F9E1' // 100% 处的颜色
              }], false)
            }
          }
        }]
      }
      this.dom = echarts.init(this.$refs.dom, 'tdTheme')
      this.dom.setOption(option)
      on(window, 'resize', this.resize)
    })
  },
  beforeDestroy () {
    off(window, 'resize', this.resize)
  }
}
</script>
