# Mixed Chart & Real-Time Examples

> Patterns not covered by single chart-type files: combining multiple series types and live-updating charts.

---

## Example 1 — Mixed Line + Bar (Dual Y-Axis)

**Use case**: Compare two metrics on different scales — e.g., precipitation (bar) vs temperature (line).  
**Editor**: [mix-line-bar](https://echarts.apache.org/examples/en/editor.html?c=mix-line-bar)

```js
const option = {
  title: { text: 'Rainfall & Temperature — 2024', left: 'center' },
  tooltip: { trigger: 'axis', axisPointer: { type: 'cross' } },
  legend: { data: ['Rainfall', 'Temperature'], bottom: 10 },
  xAxis: [
    {
      type: 'category',
      data: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
      axisPointer: { type: 'shadow' }
    }
  ],
  yAxis: [
    {
      type: 'value',
      name: 'Precipitation (mm)',
      min: 0, max: 250,
      axisLabel: { formatter: '{value} mm' }
    },
    {
      type: 'value',
      name: 'Temperature (°C)',
      min: 0, max: 30,
      position: 'right',
      axisLabel: { formatter: '{value} °C' }
    }
  ],
  series: [
    {
      name: 'Rainfall',
      type: 'bar',
      yAxisIndex: 0,
      barWidth: '40%',
      itemStyle: { color: '#73c0de', borderRadius: [4, 4, 0, 0] },
      data: [2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3]
    },
    {
      name: 'Temperature',
      type: 'line',
      yAxisIndex: 1,
      smooth: true,
      symbol: 'circle',
      symbolSize: 6,
      lineStyle: { width: 2.5, color: '#ee6666' },
      itemStyle: { color: '#ee6666' },
      data: [2.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2]
    }
  ]
};
```

---

## Example 2 — Mixed Bar + Line (KPI Dashboard)

**Use case**: Show budget (bar) alongside a trend/target line in the same chart.  
**Editor**: [bar-y-category-stack](https://echarts.apache.org/examples/en/editor.html?c=bar-y-category-stack)

```js
const categories = ['Q1', 'Q2', 'Q3', 'Q4'];
const budget   = [320000, 420000, 380000, 500000];
const actual   = [295000, 440000, 360000, 510000];
const target   = [350000, 400000, 400000, 480000];

const option = {
  title: { text: 'Budget vs Actual vs Target', left: 'center' },
  tooltip: {
    trigger: 'axis',
    axisPointer: { type: 'cross' },
    formatter: params => params.map(p =>
      `${p.marker} ${p.seriesName}: $${(p.value / 1000).toFixed(0)}k`
    ).join('<br/>')
  },
  legend: { data: ['Budget', 'Actual', 'Target'], bottom: 10 },
  xAxis: { type: 'category', data: categories },
  yAxis: [
    {
      type: 'value',
      name: 'Revenue ($)',
      axisLabel: { formatter: v => `$${(v / 1000).toFixed(0)}k` }
    }
  ],
  series: [
    {
      name: 'Budget',
      type: 'bar',
      barWidth: '25%',
      itemStyle: { color: '#91cc75', opacity: 0.8, borderRadius: [4, 4, 0, 0] },
      data: budget
    },
    {
      name: 'Actual',
      type: 'bar',
      barWidth: '25%',
      itemStyle: { color: '#5470c6', borderRadius: [4, 4, 0, 0] },
      data: actual
    },
    {
      name: 'Target',
      type: 'line',
      smooth: false,
      lineStyle: { type: 'dashed', color: '#ee6666', width: 2 },
      itemStyle: { color: '#ee6666' },
      symbol: 'diamond',
      symbolSize: 10,
      data: target
    }
  ]
};
```

---

## Example 3 — Dynamic Real-Time Chart

**Use case**: Live-updating time-series (sensor data, server metrics, stock prices).  
**Editor**: [dynamic-data2](https://echarts.apache.org/examples/en/editor.html?c=dynamic-data2)

```js
// Initialize with 50 data points
const now = Date.now();
const data = Array.from({ length: 50 }, (_, i) => ({
  time: new Date(now - (50 - i) * 2000),
  value: Math.round(Math.random() * 80 + 10)
}));

function formatRealtimeLabel(value) {
  const date = new Date(value);
  return [date.getHours(), date.getMinutes(), date.getSeconds()]
    .map(part => String(part).padStart(2, '0'))
    .join(':');
}

const chart = echarts.init(document.getElementById('chart'));

const option = {
  title: { text: 'Real-Time Server CPU (%)', left: 'center' },
  tooltip: {
    trigger: 'axis',
    axisPointer: { type: 'cross', label: { backgroundColor: '#283b56' } }
  },
  xAxis: {
    type: 'time',
    splitLine: { show: false },
    axisLabel: { formatter: val => formatRealtimeLabel(val) }
  },
  yAxis: {
    type: 'value',
    name: 'CPU %',
    min: 0, max: 100,
    splitLine: { lineStyle: { type: 'dashed' } },
    axisLine: { show: true }
  },
  visualMap: {
    show: false,
    dimension: 1,
    pieces: [
      { gt: 0,  lte: 60, color: '#91cc75' },
      { gt: 60, lte: 80, color: '#fac858' },
      { gt: 80,          color: '#ee6666' }
    ]
  },
  series: [
    {
      name: 'CPU',
      type: 'line',
      showSymbol: false,
      smooth: 0.3,
      lineStyle: { width: 2 },
      areaStyle: { opacity: 0.15 },
      data: data.map(d => [d.time, d.value])
    }
  ]
};

chart.setOption(option);

// Add a new point every 2 seconds
const timer = setInterval(() => {
  data.shift(); // remove oldest
  data.push({
    time: new Date(),
    value: Math.round(Math.random() * 80 + 10)
  });
  chart.setOption({
    series: [{ data: data.map(d => [d.time, d.value]) }]
  });
}, 2000);

// Clean up when chart is disposed
chart.on('dispose', () => clearInterval(timer));
```
