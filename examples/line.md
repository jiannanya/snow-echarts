# Line Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-line

---

## Example 1 — Smooth Area Chart with markLine & dataZoom

**Use case**: Time-series trend with average reference line and zoom slider.  
**Editor**: [area-simple](https://echarts.apache.org/examples/en/editor.html?c=area-simple)

```js
const option = {
  title: { text: 'Monthly Active Users', left: 'center' },
  tooltip: { trigger: 'axis', axisPointer: { type: 'cross' } },
  legend: { top: 30, data: ['MAU', 'DAU'] },
  grid: { left: '3%', right: '4%', bottom: '15%', containLabel: true },
  dataZoom: [
    { type: 'inside', start: 0, end: 100 },
    { type: 'slider', start: 0, end: 100, bottom: 20 }
  ],
  xAxis: {
    type: 'category',
    boundaryGap: false,
    data: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',
           'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec']
  },
  yAxis: { type: 'value', name: 'Users (k)', nameLocation: 'middle', nameGap: 50 },
  series: [
    {
      name: 'MAU',
      type: 'line',
      smooth: true,
      data: [820, 932, 901, 934, 1290, 1330, 1320, 1200, 1080, 960, 880, 950],
      areaStyle: { opacity: 0.3 },
      markLine: {
        data: [{ type: 'average', name: 'Avg' }],
        label: { formatter: 'Avg: {c}k' }
      },
      markPoint: {
        data: [
          { type: 'max', name: 'Peak' },
          { type: 'min', name: 'Valley' }
        ]
      }
    },
    {
      name: 'DAU',
      type: 'line',
      smooth: true,
      data: [200, 232, 221, 234, 390, 430, 410, 380, 310, 290, 250, 300],
      areaStyle: { opacity: 0.2 }
    }
  ]
};
```

---

## Example 2 — Gradient Stacked Area Chart

**Use case**: Show cumulative composition over time with visual gradient fills.  
**Editor**: [area-stack-gradient](https://echarts.apache.org/examples/en/editor.html?c=area-stack-gradient)

```js
const option = {
  title: { text: 'Channel Attribution (Stacked)', left: 'center' },
  tooltip: { trigger: 'axis' },
  legend: { bottom: 10, data: ['Organic', 'Paid', 'Referral', 'Direct'] },
  grid: { left: '3%', right: '4%', bottom: '12%', containLabel: true },
  xAxis: {
    type: 'category',
    boundaryGap: false,
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
  },
  yAxis: { type: 'value' },
  series: [
    {
      name: 'Organic',
      type: 'line',
      stack: 'channels',
      smooth: true,
      lineStyle: { width: 0 },
      areaStyle: {
        color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
          { offset: 0, color: 'rgba(128, 255, 165)' },
          { offset: 1, color: 'rgba(1, 191, 236)' }
        ])
      },
      emphasis: { focus: 'series' },
      data: [140, 232, 101, 264, 90, 340, 250]
    },
    {
      name: 'Paid',
      type: 'line',
      stack: 'channels',
      smooth: true,
      lineStyle: { width: 0 },
      areaStyle: {
        color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
          { offset: 0, color: 'rgba(0, 221, 255)' },
          { offset: 1, color: 'rgba(77, 119, 255)' }
        ])
      },
      emphasis: { focus: 'series' },
      data: [120, 282, 111, 234, 220, 340, 310]
    },
    {
      name: 'Referral',
      type: 'line',
      stack: 'channels',
      smooth: true,
      lineStyle: { width: 0 },
      areaStyle: {
        color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
          { offset: 0, color: 'rgba(55, 162, 255)' },
          { offset: 1, color: 'rgba(116, 21, 219)' }
        ])
      },
      emphasis: { focus: 'series' },
      data: [320, 132, 201, 334, 190, 130, 220]
    },
    {
      name: 'Direct',
      type: 'line',
      stack: 'channels',
      smooth: true,
      lineStyle: { width: 0 },
      areaStyle: {
        color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
          { offset: 0, color: 'rgba(255, 191, 0)' },
          { offset: 1, color: 'rgba(224, 62, 76)' }
        ])
      },
      emphasis: { focus: 'series' },
      data: [220, 402, 231, 134, 190, 230, 120]
    }
  ]
};
```

---

## Example 3 — Multi-Axis Line (Dual Y-Axis)

**Use case**: Compare metrics with different units/scales on the same timeline.  
**Editor**: [multiple-y-axis](https://echarts.apache.org/examples/en/editor.html?c=multiple-y-axis)

```js
const option = {
  title: { text: 'Revenue vs Conversion Rate', left: 'center' },
  tooltip: { trigger: 'axis' },
  legend: { top: 30, data: ['Revenue ($k)', 'Conv. Rate (%)'] },
  grid: { left: '3%', right: '6%', bottom: '3%', containLabel: true },
  xAxis: {
    type: 'category',
    data: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun']
  },
  yAxis: [
    {
      type: 'value',
      name: 'Revenue ($k)',
      position: 'left',
      axisLabel: { formatter: '${value}k' }
    },
    {
      type: 'value',
      name: 'Conv. Rate (%)',
      position: 'right',
      min: 0,
      max: 10,
      axisLabel: { formatter: '{value}%' }
    }
  ],
  series: [
    {
      name: 'Revenue ($k)',
      type: 'line',
      yAxisIndex: 0,
      smooth: true,
      data: [120, 180, 150, 220, 200, 260],
      itemStyle: { color: '#5470c6' }
    },
    {
      name: 'Conv. Rate (%)',
      type: 'line',
      yAxisIndex: 1,
      smooth: true,
      data: [3.2, 4.5, 3.8, 5.1, 4.9, 6.2],
      lineStyle: { type: 'dashed' },
      itemStyle: { color: '#ee6666' }
    }
  ]
};
```
