<template>
  <div ref="chartContainer" class="echart-container"></div>
</template>

<script lang="ts" setup>
import { onMounted } from 'vue'
import { useEChart } from '../../src/hooks';

  const { chartContainer, setChartOption } = useEChart()

    const renderChart = () => {
      const option = {
        grid: {
          top: '32',
          left: '0%',
          right: '0%',
          bottom: '0%',
          containLabel: true,
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'none',
          },
          extraCssText: 'border-radius: 0;',
        },
        legend: {
          data: ['水能', '煤炭', '风能', '太阳能', '生物能'],
          right: '2%',
          top: 'top',
          itemWidth: 10,
          itemHeight: 1,
          itemGap: 16,
          icon: 'rect',
          textStyle: {
            fontSize: 12,
            color: 'rgba(128, 128, 160, 0.65)',
          },
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
          splitNumber: 3,
          splitLine: {
            lineStyle: {
              type: 'dashed',
              color: 'rgba(128, 128, 160, 0.15)',
            },
          },
          axisLabel: {
            fontSize: 12,
            color: 'rgba(128, 128, 160, 0.65)',
            lineHeight: 20,
          },
          type: 'value',
        },
        series: [{
          itemStyle: {
            color: '#009EF7',
          },
          symbolSize: 0,
          lineStyle: {
            width: 1,
          },
          name: '水能',
          data: [20, 30, 18, 36, 40, 50, 70, 80],
          type: 'line',
        }, {
          itemStyle: {
            color: '#20C97D',
          },
          symbolSize: 0,
          lineStyle: {
            width: 1,
          },
          name: '煤炭',
          data: [10, 20, 48, 66, 10, 40, 30, 20],
          type: 'line',
        }, {
          itemStyle: {
            color: '#6D75F9',
          },
          symbolSize: 0,
          lineStyle: {
            width: 1,
          },
          name: '风能',
          data: [15, 35, 29, 35, 45, 55, 25, 85],
          type: 'line',
        }, {
          itemStyle: {
            color: '#F2C937',
          },
          symbolSize: 0,
          lineStyle: {
            width: 1,
          },
          name: '太阳能',
          data: [12, 50, 18, 66, 43, 30, 20, 30],
          type: 'line',
        }, {
          itemStyle: {
            color: '#DE78EC',
          },
          symbolSize: 0,
          lineStyle: {
            width: 1,
          },
          name: '生物能',
          data: [60, 34, 19, 31, 65, 52, 42, 89],
          type: 'line',
        }],
      }
      setChartOption(option)
    }

    onMounted(() => {
      renderChart()
    })
</script>


<style>
  body {
    padding: var(--lg)
  }
.echart-container {
  min-height: 200px;
}
</style>
