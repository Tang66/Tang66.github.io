<template>
  <div ref="chartContainer" class="echart-container"></div>
</template>

<script lang="ts" setup>
import { onMounted } from 'vue'
import { useEChart } from '../../src/hooks';
import * as echarts from 'echarts'
  
  const { chartContainer, setChartOption } = useEChart()

    const renderChart = () => {
      const option = {
        grid: {
          top: 0,
          bottom: 26,
          left: 0,
          right: 0,
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'none',
          },
          extraCssText: 'border-radius: 0;',
          formatter: (params: any) => `
          <div style="backgroundColor:#fff;borderRaduis:0">
            ${params[0].marker}
            <span>${params[0].axisValue} <span style="font-weight: bold; margin-left: 30px">${params[0].value}</span></span>
          </div>
          `,
        },
        xAxis: {
          axisLabel: {
            fontSize: 12,
            color: 'rgba(128, 128, 160, 0.65)',
            lineHeight: 20,
            margin: 5,
          },
          axisTick: {
            alignWithLabel: true,
          },
          axisLine: {
            lineStyle: {
              color: 'rgba(128, 128, 160, 0.15)',
            },
          },
          type: 'category',
          data: ['2002', '2004', '2006', '2008', '2010', '2012', '2014', '2016'],
        },
        yAxis: {
          show: false,
          type: 'value',
        },
        series: [{
          itemStyle: {
            color: new echarts.graphic.LinearGradient(
              0, 0, 0, 1,
              [
                { offset: 0, color: '#009EF7' },
                { offset: 0.04, color: '#009EF7' },
                { offset: 1, color: 'rgba(128, 128, 160, 0)' },
              ],
            ),
            borderRadius: [2, 2, 0, 0],
          },
          barWidth: 24,
          showBackground: true,
          backgroundStyle: {
            color: 'rgba(128, 128, 160, 0.1)',
          },
          data: [20, 60, 40, 90, 60, 70, 10, 40],
          type: 'bar',
        }],
      }
      setChartOption(option)
    }

    onMounted(() => {
      renderChart()
    })
</script>


<style>
.echart-container {
  min-height: 200px;
}
</style>
