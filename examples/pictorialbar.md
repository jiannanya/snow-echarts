# PictorialBar Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-pictorialBar

---

## Example 1 — Repeating Icon Bar (Person Icons)

**Use case**: Infographic-style bar chart where icons repeat to represent quantity.  
**Editor**: [pictorialBar-spirit](https://echarts.apache.org/examples/en/editor.html?c=pictorialBar-spirit)

```js
const option = {
  title: { text: 'Population by Country (pictorialBar)', left: 'center' },
  tooltip: {
    trigger: 'axis',
    axisPointer: { type: 'shadow' },
    formatter: params => `${params[0].name}: ${params[0].value}M`
  },
  xAxis: {
    type: 'category',
    data: ['China', 'India', 'USA', 'Indonesia', 'Pakistan', 'Brazil'],
    axisLabel: { fontSize: 12 }
  },
  yAxis: {
    type: 'value',
    name: 'Population (M)',
    max: 1500
  },
  series: [
    {
      type: 'pictorialBar',
      barWidth: '60%',
      // SVG path: simple person silhouette
      symbol: 'path://M0,10 L5,0 L10,10 L7,10 L7,20 L3,20 L3,10 Z',
      symbolSize: ['80%', '90%'],
      symbolRepeat: true,
      symbolMargin: '10%',
      itemStyle: { opacity: 0.9 },
      emphasis: {
        itemStyle: { opacity: 1 }
      },
      label: {
        show: true,
        position: 'top',
        formatter: '{c}M',
        fontWeight: 'bold'
      },
      data: [
        { value: 1412, name: 'China',     itemStyle: { color: '#ee6666' } },
        { value: 1380, name: 'India',     itemStyle: { color: '#fac858' } },
        { value: 331,  name: 'USA',       itemStyle: { color: '#5470c6' } },
        { value: 273,  name: 'Indonesia', itemStyle: { color: '#91cc75' } },
        { value: 220,  name: 'Pakistan',  itemStyle: { color: '#73c0de' } },
        { value: 215,  name: 'Brazil',    itemStyle: { color: '#3ba272' } }
      ]
    }
  ]
};
```

---

## Example 2 — Dotted / Staged Bar

**Use case**: Show discrete units stacked vertically — useful for showing capacity vs. usage.  
**Editor**: [pictorialBar-dotted](https://echarts.apache.org/examples/en/editor.html?c=pictorialBar-dotted)

```js
const totalCapacity = [10, 10, 10, 10, 10];
const usedCapacity  = [7, 5, 9, 3, 8];
const categories    = ['Server A', 'Server B', 'Server C', 'Server D', 'Server E'];

const option = {
  title: { text: 'Server Capacity Utilization', left: 'center' },
  tooltip: {
    trigger: 'axis',
    formatter: params => {
      const used  = params.find(p => p.seriesName === 'Used');
      const total = params.find(p => p.seriesName === 'Total');
      return `${used.name}<br/>
        Used: ${used.value} / ${total.value} slots<br/>
        Utilization: ${Math.round(used.value / total.value * 100)}%`;
    }
  },
  legend: { data: ['Total', 'Used'], bottom: 10 },
  xAxis: { type: 'category', data: categories },
  yAxis: { type: 'value', name: 'Slots', max: 12, splitLine: { show: false } },
  series: [
    {
      name: 'Total',
      type: 'pictorialBar',
      symbol: 'rect',
      symbolSize: [24, 10],
      symbolMargin: 4,
      symbolRepeat: true,
      itemStyle: { color: '#ddd', opacity: 1 },
      data: totalCapacity,
      z: 1
    },
    {
      name: 'Used',
      type: 'pictorialBar',
      symbol: 'rect',
      symbolSize: [24, 10],
      symbolMargin: 4,
      symbolRepeat: true,
      label: {
        show: true,
        position: 'top',
        formatter: p => `${Math.round(p.value / totalCapacity[p.dataIndex] * 100)}%`
      },
      data: usedCapacity.map((v, i) => ({
        value: v,
        itemStyle: {
          color: v / totalCapacity[i] > 0.8 ? '#ee6666' :
                 v / totalCapacity[i] > 0.5 ? '#fac858' : '#91cc75'
        }
      })),
      z: 2
    }
  ]
};
```

---

## Example 3 — Body Fill (Water-Level)

**Use case**: Show percentage as a fill level inside a shaped icon.  
**Editor**: [pictorialBar-body-fill](https://echarts.apache.org/examples/en/editor.html?c=pictorialBar-body-fill)

```js
const waterDropPath = 'path://M20,0 Q30,20 30,30 A15,15,0,0,1,10,30 Q10,20 20,0Z';

const option = {
  title: { text: 'Quarterly Goals Achievement', left: 'center' },
  tooltip: {
    formatter: params => `${params.name}: ${params.value}% achieved`
  },
  xAxis: {
    type: 'category',
    data: ['Revenue', 'New Clients', 'Support SLA', 'NPS Score', 'Retention'],
    axisLabel: { fontSize: 11 }
  },
  yAxis: { type: 'value', max: 100, name: '% Achieved', show: false },
  series: [
    // Background (100% gray) to show the "empty" part
    {
      type: 'pictorialBar',
      symbol: waterDropPath,
      symbolSize: ['120%', '100%'],
      symbolOffset: [0, 0],
      itemStyle: { color: '#eee' },
      z: 1,
      data: [100, 100, 100, 100, 100]
    },
    // Actual progress fill
    {
      type: 'pictorialBar',
      symbol: waterDropPath,
      symbolSize: ['120%', '100%'],
      symbolOffset: [0, 0],
      symbolClip: true,       // clip to the icon shape
      itemStyle: { opacity: 0.8 },
      label: {
        show: true,
        position: 'inside',
        formatter: '{c}%',
        color: '#fff',
        fontWeight: 'bold',
        fontSize: 13
      },
      z: 2,
      data: [
        { value: 85, itemStyle: { color: '#91cc75' } },
        { value: 62, itemStyle: { color: '#fac858' } },
        { value: 95, itemStyle: { color: '#5470c6' } },
        { value: 48, itemStyle: { color: '#ee6666' } },
        { value: 90, itemStyle: { color: '#73c0de' } }
      ]
    }
  ]
};
```
