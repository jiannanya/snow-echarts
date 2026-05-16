# Custom Series Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-custom

The `custom` series type lets you define arbitrary visual elements via a `renderItem` callback.  
All shapes are drawn using ECharts' `zrender` graphic API.

---

## Example 1 — Gantt Chart

**Use case**: Project timeline with tasks spanning date ranges across rows.  
**Editor**: [custom-gantt-flight](https://echarts.apache.org/examples/en/editor.html?c=custom-gantt-flight)

```js
const categories = ['Design', 'Development', 'Testing', 'Deployment', 'Marketing'];
const tasks = [
  { name: 'UI Wireframes',     category: 0, start: '2024-01-05', end: '2024-01-20' },
  { name: 'DB Schema',         category: 1, start: '2024-01-10', end: '2024-01-25' },
  { name: 'Frontend Dev',      category: 1, start: '2024-01-21', end: '2024-02-15' },
  { name: 'Backend API',       category: 1, start: '2024-01-15', end: '2024-02-10' },
  { name: 'Unit Tests',        category: 2, start: '2024-02-05', end: '2024-02-20' },
  { name: 'Integration Tests', category: 2, start: '2024-02-18', end: '2024-03-01' },
  { name: 'Staging Deploy',    category: 3, start: '2024-03-01', end: '2024-03-07' },
  { name: 'Production',        category: 3, start: '2024-03-08', end: '2024-03-10' },
  { name: 'Launch Campaign',   category: 4, start: '2024-03-08', end: '2024-03-31' }
];

const colors = ['#5470c6', '#91cc75', '#fac858', '#ee6666', '#73c0de'];

const option = {
  title: { text: 'Project Timeline', left: 'center' },
  tooltip: {
    formatter: params => {
      const d = params.data;
      return `<b>${d[3]}</b><br/>Start: ${d[1]}<br/>End: ${d[2]}`;
    }
  },
  xAxis: {
    type: 'time',
    min: '2024-01-01',
    max: '2024-04-01',
    scale: true,
    axisLabel: { formatter: val => echarts.format.formatTime('MM-dd', val) }
  },
  yAxis: {
    type: 'category',
    data: categories,
    inverse: true
  },
  grid: { left: 100 },
  series: [
    {
      type: 'custom',
      renderItem: (params, api) => {
        const categoryIndex = api.value(0);
        const start  = api.coord([api.value(1), categoryIndex]);
        const end    = api.coord([api.value(2), categoryIndex]);
        const height = api.size([0, 1])[1] * 0.6;
        const x      = start[0];
        const y      = start[1] - height / 2;
        const width  = end[0] - start[0];
        return {
          type: 'rect',
          shape: { x, y, width, height, r: 4 },
          style: {
            fill: colors[categoryIndex],
            opacity: 0.85
          },
          emphasis: {
            style: { opacity: 1, shadowBlur: 6, shadowColor: 'rgba(0,0,0,0.3)' }
          }
        };
      },
      encode: { x: [1, 2], y: 0 },
      data: tasks.map(t => [t.category, t.start, t.end, t.name])
    }
  ]
};
```

---

## Example 2 — Error Bars on Scatter

**Use case**: Show measurement uncertainty by drawing error bars through a `custom` overlay.  
**Editor**: [custom-error-bar](https://echarts.apache.org/examples/en/editor.html?c=custom-error-bar)

```js
// [x, y, errorLow, errorHigh]
const measurements = [
  [1, 30, 25, 35], [2, 45, 40, 52], [3, 38, 33, 44],
  [4, 52, 47, 58], [5, 60, 54, 67], [6, 55, 48, 62],
  [7, 70, 64, 76], [8, 65, 58, 72], [9, 78, 71, 85]
];

const option = {
  title: { text: 'Experimental Results with Error Bars', left: 'center' },
  tooltip: {
    formatter: params => params.componentType === 'series' && params.seriesType === 'scatter'
      ? `x=${params.data[0]}, y=${params.data[1]}`
      : ''
  },
  xAxis: { type: 'value', name: 'Sample #', min: 0, max: 10 },
  yAxis: { type: 'value', name: 'Value', min: 20, max: 100 },
  series: [
    {
      type: 'scatter',
      symbolSize: 10,
      itemStyle: { color: '#5470c6' },
      data: measurements.map(d => [d[0], d[1]])
    },
    {
      type: 'custom',
      itemStyle: { color: '#5470c6' },
      renderItem: (params, api) => {
        const x   = api.value(0);
        const lo  = api.value(2);
        const hi  = api.value(3);
        const cx  = api.coord([x, api.value(1)])[0];
        const yLo = api.coord([x, lo])[1];
        const yHi = api.coord([x, hi])[1];
        const hw  = 5; // half-width of caps
        return {
          type: 'group',
          children: [
            // Vertical line
            { type: 'line', shape: { x1: cx, y1: yLo, x2: cx, y2: yHi },
              style: { stroke: '#5470c6', lineWidth: 2 } },
            // Bottom cap
            { type: 'line', shape: { x1: cx - hw, y1: yLo, x2: cx + hw, y2: yLo },
              style: { stroke: '#5470c6', lineWidth: 2 } },
            // Top cap
            { type: 'line', shape: { x1: cx - hw, y1: yHi, x2: cx + hw, y2: yHi },
              style: { stroke: '#5470c6', lineWidth: 2 } }
          ]
        };
      },
      data: measurements
    }
  ]
};
```

---

## Example 3 — Custom Polar Heatmap

**Use case**: Map category × hour data onto a polar coordinate grid using custom rectangles.  
**Editor**: [custom-polar-heatmap](https://echarts.apache.org/examples/en/editor.html?c=custom-polar-heatmap)

```js
const days  = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
const hours = Array.from({ length: 24 }, (_, i) => `${i}:00`);

const data = days.flatMap((day, di) =>
  hours.map((_, hi) => [di, hi, Math.round(Math.random() * 80 + (hi >= 9 && hi <= 18 ? 20 : 0))])
);

const option = {
  title: { text: 'Weekly Activity by Hour', left: 'center' },
  tooltip: {
    formatter: p => `${days[p.data[0]]}, ${hours[p.data[1]]}: ${p.data[2]} events`
  },
  visualMap: {
    min: 0, max: 100,
    orient: 'horizontal',
    left: 'center',
    bottom: 10,
    inRange: { color: ['#313695', '#4575b4', '#74add1', '#abd9e9', '#e0f3f8', '#ffffbf', '#fee090', '#fdae61', '#f46d43', '#d73027', '#a50026'] }
  },
  grid: { left: 60, right: 20, top: 60, bottom: 60 },
  xAxis: { type: 'category', data: hours, axisLabel: { interval: 3 } },
  yAxis: { type: 'category', data: days },
  series: [
    {
      type: 'heatmap',
      data: data,
      label: { show: false },
      emphasis: { itemStyle: { shadowBlur: 10, shadowColor: 'rgba(0,0,0,0.5)' } }
    }
  ]
};
```
