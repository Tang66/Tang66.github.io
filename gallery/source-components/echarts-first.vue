<template>
  <div ref="chartContainer" class="echart-container"></div>
</template>

<script lang="ts" setup>
import { onMounted, PropType } from 'vue'
import * as echarts from 'echarts'
import { useEChart } from '../../src/hooks';

const props = defineProps({
  chartData: {
    type: Array as PropType<Array<{ label: string; value: string; color: string | string[]; }>>,
    default: () => [
      { label: '沣西新城', value: 20, color: ['rgba(114,245,172,0.00)', 'rgba(114,245,172,0.56)'] },
      { label: '沣东新城', value: 60, color: ['rgba(37,129,255,0.00)', 'rgba(37,129,255,0.56)'] },
      { label: '秦汉新城', value: 80, color: ['rgba(255,234,68,0.00)', 'rgba(255,234,68,0.56)'] },
      { label: '泾河新城', value: 100, color: ['rgba(255,84,84,0.0)', 'rgba(255,84,84,0.56)'] },
      { label: '泾河新城', value: 40, color: ['rgba(253,137,47,0.00)', 'rgba(253,137,47,0.56)'] },
    ],
  },
})

const { chartContainer, setChartOption } = useEChart()
const renderChart = () => {
  const option = {
    legend: {
      data: props.chartData.map(d => d.label),
      bottom: '0',
      icon: 'rect',
      itemHeight: 12,
      itemWidth: 12,
      itemGap: 16,
      textStyle: {
        'color': '#6F8EA8',
      },
    },
    series: [{
      type: 'funnel',
      left: '10%',
      top: 0,
      bottom: 45,
      width: '80%',
      sort: 'ascending',
      gap: 2,
      label: {
        show: false,
        position: 'inside',
      },
      emphasis: {
        label: {
          color: '#fff',
          fontSize: 14,
          formatter: '{c}',
          backgroundColor: 'transparent',
          fontWeight: 'bold',
        },
        labelLine: {
          show: false,
        },
      },
      data: props.chartData.map(d => ({
        value: d.value,
        name: d.label,
        itemStyle: {
          color: typeof d.color === 'string' ? d.color : new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            { offset: 0, color: d.color[0] },
            { offset: 1, color: d.color[1] },
          ]),
          borderWidth: 0,
          borderRadius: [2, 2, 0, 0],
        },
      })),
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
  width: 500px;
  height: 300px;
}
</style>
