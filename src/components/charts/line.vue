<template>
  <div ref="dom" class="charts chart-bar"></div>
</template>

<script>
import echarts from 'echarts'
import tdTheme from './theme.json'
import { on, off } from '@/libs/tools'
echarts.registerTheme('tdTheme', tdTheme)
export default {
  name: 'ChartLine',
  props: {
    value: Array,
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
    },
    hexToRgba (hex, opacity) {
      let rgbaColor = ''
      let reg = /^#[\da-f]{6}$/i
      if (reg.test(hex)) {
        rgbaColor = `rgba(${parseInt('0x' + hex.slice(1, 3))},${parseInt(
          '0x' + hex.slice(3, 5)
        )},${parseInt('0x' + hex.slice(5, 7))},${opacity})`
      }
      return rgbaColor
    }
  },
  mounted () {
    let xAxisData = ['1', '2', '3', '4', '5', '6', '7', '8']
    let yAxisData1 = [100, 138, 350, 173, 180, 150, 180, 230]
    let yAxisData2 = [233, 233, 200, 180, 199, 233, 210, 180]
    let color = [
      '#8B5CFF',
      '#00CA69'
    ]
    this.$nextTick(() => {
    //   let xAxisData = Object.keys(this.value)
      let option = {
        backgroundColor: '#fff',
        color: color,
        tooltip: {
          trigger: 'axis',
          formatter: function (params) {
            let html = ''
            params.forEach(v => {
              html += `<div style="color: #666;font-size: 14px;line-height: 24px">
                <span style="display:inline-block;margin-right:5px;border-radius:10px;width:10px;height:10px;background-color:${color[v.componentIndex]};"></span>
                ${v.seriesName}2020.${v.name}  
                <span style="color:${color[v.componentIndex]};font-weight:700;font-size: 18px;margin-left:5px">${v.value}</span>
                万元`
            })
            return html
          },
          extraCssText: 'background: #fff; border-radius: 0;box-shadow: 0 0 3px rgba(0, 0, 0, 0.2);color: #333;',
          axisPointer: {
            type: 'shadow',
            shadowStyle: {
              color: '#ffffff',
              shadowColor: 'rgba(225,225,225,1)',
              shadowBlur: 5
            }
          }
        },
        grid: {
          top: 10,
          bottom: 20,
          left: 0,
          right: 0
        //   containLabel: true
        },
        xAxis: [{
          type: 'category',
          offset: -1,
          boundaryGap: false,
          axisLabel: {
            formatter: '{value}',
            textStyle: {
              color: '#333',
              fontSize: 7
            }
          },
          splitLine: {
            show: false,
            lineStyle: {
              type: 'dashed',
              color: '#E9E9E9'
            }
          },
          axisLine: {
            show: false,
            lineStyle: {
              color: '#D9D9D9'
            }
          },
          data: xAxisData
        }],
        yAxis: [{
          position: 'right',
          offset: -20,
          type: 'value',
          axisLabel: {
            textStyle: {
              color: '#666',
              fontSize: 7
            }
          },
          nameTextStyle: {
            color: '#666',
            fontSize: 12,
            lineHeight: 40
          },
          // 分割线
          splitLine: {
            lineStyle: {
              color: '#E9E9E9'
            }
          },
          axisLine: {
            show: false
          },
          axisTick: {
            show: false
          }
        }],
        series: [{
        // name: "2018",
          name: '预测出电量',
          type: 'line',
          smooth: true,
          symbolSize: 3,
          zlevel: 3,
          lineStyle: {
            normal: {
              color: color[0],
              shadowBlur: 3,
              shadowColor: this.hexToRgba(color[0], 0.5),
              shadowOffsetY: 8
            }
          },
          symbol: 'circle', // 数据交叉点样式
          areaStyle: {
            normal: {
              color: new echarts.graphic.LinearGradient(
                0,
                0,
                0,
                1,
                [{
                  offset: 0,
                  color: this.hexToRgba(color[0], 0.3)
                },
                {
                  offset: 1,
                  color: this.hexToRgba(color[0], 0.1)
                }
                ],
                false
              ),
              shadowColor: this.hexToRgba(color[0], 0.1),
              shadowBlur: 10
            }
          },
          data: yAxisData1
        }, {
          name: '实际用电量',
          type: 'line',
          smooth: true,
          symbolSize: 3,
          zlevel: 3,
          lineStyle: {
            normal: {
              color: color[1],
              shadowBlur: 3,
              shadowColor: this.hexToRgba(color[1], 0.5),
              shadowOffsetY: 8
            }
          },
          symbol: 'circle', // 数据交叉点样式 (实心点)
          areaStyle: {
            normal: {
              color: new echarts.graphic.LinearGradient(
                0,
                0,
                0,
                1,
                [{
                  offset: 0,
                  color: this.hexToRgba(color[1], 0.3)
                },
                {
                  offset: 1,
                  color: this.hexToRgba(color[1], 0.1)
                }
                ],
                false
              ),
              shadowColor: this.hexToRgba(color[1], 0.1),
              shadowBlur: 10
            }
          },
          data: yAxisData2
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
