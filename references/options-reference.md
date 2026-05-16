# ECharts Options Reference

Detailed configuration for common ECharts components.

---

## `title`

```js
title: {
  text: 'Main Title',
  subtext: 'Subtitle',
  left: 'center',     // 'left'|'center'|'right'|px|'%'
  top: 'auto',        // 'top'|'middle'|'bottom'|px|'%'
  textStyle: { fontSize: 18, fontWeight: 'bold', color: '#333' },
  subtextStyle: { fontSize: 12, color: '#aaa' },
  show: true
}
```

---

## `legend`

```js
legend: {
  show: true,
  type: 'plain',      // 'plain'|'scroll' (scroll when many items)
  orient: 'horizontal', // 'horizontal'|'vertical'
  left: 'center',
  top: 'bottom',
  data: ['Series A', 'Series B'],  // optional: auto-derived from series names
  selected: { 'Series A': true, 'Series B': false },
  itemWidth: 25,
  itemHeight: 14,
  icon: 'circle',     // 'circle'|'rect'|'roundRect'|'triangle'|'diamond'|'pin'|'arrow'|'none'
  formatter: (name) => name + ' (%)',
  textStyle: { color: '#555' },
  inactiveColor: '#ccc'
}
```

---

## `grid`

Defines the cartesian coordinate layout area.

```js
grid: {
  left: '10%',    // or px
  right: '10%',
  top: 60,
  bottom: 60,
  containLabel: true  // include axis labels in the grid area (prevents clipping)
}
// Multiple grids:
grid: [
  { left: '5%', width: '40%' },
  { right: '5%', width: '40%' }
]
```

---

## `xAxis` / `yAxis`

```js
xAxis: {
  type: 'category',  // 'category'|'value'|'time'|'log'
  data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri'],  // for type:'category'
  name: 'Day',
  nameLocation: 'middle',  // 'start'|'middle'|'end'
  nameGap: 30,
  boundaryGap: true,   // padding on both sides (false for line charts)
  inverse: false,
  min: 0, max: 'dataMax',  // 'dataMin'|'dataMax'|number
  splitNumber: 5,
  axisLabel: {
    rotate: 45,
    formatter: (val) => val.substring(0, 3),
    interval: 0    // 0 = show all; 'auto'
  },
  axisLine: { show: true, lineStyle: { color: '#999' } },
  splitLine: { show: true, lineStyle: { type: 'dashed' } },
  axisTick: { show: true },
  gridIndex: 0  // link to specific grid
}
```

**Axis types:**
- `'category'`: discrete labels, use `data: [...]`
- `'value'`: continuous numeric
- `'time'`: timestamp-aware (ISO strings, Unix ms, Date objects)
- `'log'`: logarithmic scale — set `logBase: 10`

---

## `tooltip`

```js
tooltip: {
  show: true,
  trigger: 'axis',    // 'item'|'axis'|'none'
  axisPointer: {
    type: 'cross',    // 'line'|'shadow'|'cross'|'none'
    crossStyle: { color: '#999' }
  },
  formatter: '{a}<br/>{b}: {c}',
  // or function:
  formatter: (params) => {
    // params is array (trigger:'axis') or object (trigger:'item')
    return `<b>${params.name}</b>: ${params.value}`;
  },
  backgroundColor: 'rgba(255,255,255,0.9)',
  borderColor: '#ccc',
  borderWidth: 1,
  padding: [5, 10],
  textStyle: { color: '#333', fontSize: 13 },
  enterable: false    // allow mouse into tooltip
}
```

**Formatter template strings:**
| Placeholder | Meaning |
|---|---|
| `{a}` | Series name |
| `{b}` | Data name / category |
| `{c}` | Value |
| `{d}` | Percentage (pie) |
| `{e}` | Data name |
| `{@fieldName}` | Dataset field value |

---

## `toolbox`

```js
toolbox: {
  show: true,
  feature: {
    saveAsImage: { title: 'Save', name: 'chart', type: 'png' },
    dataZoom: { yAxisIndex: 'none', title: { zoom: 'Zoom', back: 'Reset' } },
    dataView: { readOnly: false, title: 'Data View' },
    magicType: { type: ['line', 'bar', 'stack'], title: { line:'Line', bar:'Bar', stack:'Stack' } },
    restore: { title: 'Restore' },
    brush: {}
  },
  right: 15,
  top: 15,
  iconStyle: { borderColor: '#666' }
}
```

---

## `dataZoom`

Enables scrolling / range-selecting on axes.

```js
dataZoom: [
  {
    type: 'slider',      // slider bar below chart
    xAxisIndex: 0,       // which axis to zoom (or [0,1] for multiple)
    start: 0,            // percentage 0-100
    end: 50,
    height: 20,
    bottom: 10
  },
  {
    type: 'inside',      // mouse-wheel / pinch zoom
    xAxisIndex: 0,
    start: 0,
    end: 100
  }
]
```

---

## `visualMap`

Maps data values to visual properties (color, size, opacity).

```js
// Continuous (gradient)
visualMap: {
  type: 'continuous',
  min: 0,
  max: 100,
  calculable: true,
  orient: 'vertical',
  left: 'right',
  top: 'center',
  inRange: {
    color: ['#313695', '#4575b4', '#74add1', '#abd9e9',
            '#e0f3f8', '#ffffbf', '#fee090', '#fdae61',
            '#f46d43', '#d73027', '#a50026']
  }
}

// Piecewise (discrete)
visualMap: {
  type: 'piecewise',
  pieces: [
    { min: 0, max: 30, label: 'Low', color: '#93CE07' },
    { min: 30, max: 70, label: 'Medium', color: '#FBDB0F' },
    { min: 70, max: 100, label: 'High', color: '#FC7D02' }
  ]
}
```

---

## `series[i].label`

Controls data point labels.

```js
label: {
  show: true,
  position: 'top',     // 'top'|'bottom'|'left'|'right'|'inside'|'insideTop'|[x,y]
  formatter: '{b}: {c}',
  // or function: (params) => params.value.toFixed(2)
  fontSize: 12,
  color: '#333',
  fontWeight: 'normal',
  rotate: 0,
  distance: 5,
  padding: [3, 5],
  backgroundColor: 'rgba(0,0,0,0.1)',
  borderRadius: 3
}
```

---

## `series[i].itemStyle`

```js
itemStyle: {
  color: '#5470c6',     // or function: (params) => colorMap[params.name]
  borderColor: '#fff',
  borderWidth: 1,
  borderRadius: [4, 4, 0, 0],   // bar rounded tops
  opacity: 0.8,
  shadowBlur: 10,
  shadowColor: 'rgba(0,0,0,0.2)'
}
```

**Color by category (dynamic):**
```js
itemStyle: {
  color: (params) => {
    const colors = ['#5470c6', '#91cc75', '#fac858', '#ee6666'];
    return colors[params.dataIndex % colors.length];
  }
}
```

---

## `series[i].emphasis`

Hover/highlight state.

```js
emphasis: {
  disabled: false,
  scale: true,           // scale on hover
  focus: 'series',       // 'none'|'self'|'series'|'adjacency' (graph)
  itemStyle: { color: '#264fc5', shadowBlur: 20 },
  label: { show: true, fontSize: 14, fontWeight: 'bold' }
}
```

---

## `dataset`

Decouples data from configuration:

```js
dataset: {
  dimensions: ['product', 'Jan', 'Feb', 'Mar'],
  source: [
    { product: 'Matcha Latte', Jan: 86, Feb: 95, Mar: 101 },
    { product: 'Milk Tea',     Jan: 95, Feb: 102, Mar: 120 },
    // or array form:
    ['Milk Tea', 95, 102, 120]
  ]
}
// Then series: [{ type: 'bar', seriesLayoutBy: 'row' }]
// No need for data field in series when using dataset
```

---

## `markPoint` / `markLine` / `markArea`

```js
markPoint: {
  data: [
    { type: 'max', name: 'Max Value' },
    { type: 'min', name: 'Min Value' },
    { coord: [3, 200], name: 'Custom' }
  ]
},
markLine: {
  data: [
    { type: 'average', name: 'Avg' },
    [{ coord: [0, 150] }, { coord: [4, 150] }]  // fixed line
  ],
  lineStyle: { type: 'dashed', color: 'red' }
},
markArea: {
  data: [[{ xAxis: 'Mon' }, { xAxis: 'Wed' }]],
  itemStyle: { color: 'rgba(255,0,0,0.1)' }
}
```

---

## `color` — Global Color Palette

```js
color: ['#5470c6', '#91cc75', '#fac858', '#ee6666', '#73c0de',
        '#3ba272', '#fc8452', '#9a60b4', '#ea7ccc']
```

---

## Animation

```js
animation: true,
animationDuration: 1000,
animationEasing: 'cubicOut',     // 'linear'|'quadraticIn'|'elasticOut'|etc.
animationDelay: (idx) => idx * 100,
animationDurationUpdate: 300,
animationEasingUpdate: 'cubicInOut'
```

Disable for performance with large data:
```js
animation: false
```

---

## Theme

Built-in themes: `'dark'`

```js
// Use built-in dark theme
echarts.init(dom, 'dark');

// Register custom theme
echarts.registerTheme('myTheme', {
  color: ['#dd6b66', '#759aa0', '#e69d87'],
  backgroundColor: '#1a1a2e',
  textStyle: { color: '#eee' }
});
echarts.init(dom, 'myTheme');
```

---

## Responsive Layout

```js
// Use media queries
media: [
  {
    query: { maxWidth: 600 },
    option: {
      legend: { orient: 'vertical', left: 0 },
      grid: { left: '20%' }
    }
  }
]
```

---

## `geo` Component

```js
geo: {
  map: 'china',         // must be pre-registered via echarts.registerMap()
  roam: true,           // enable pan & zoom
  zoom: 1.2,
  center: [104, 37],
  itemStyle: {
    areaColor: '#e7dfe6',
    borderColor: '#aaa',
    borderWidth: 0.5
  },
  emphasis: {
    itemStyle: { areaColor: '#6b8cca' },
    label: { show: true }
  },
  regions: [
    { name: 'Beijing', itemStyle: { areaColor: 'red' } }
  ]
}
```

---

## Event Handling

```js
// Common events: 'click', 'dblclick', 'mouseover', 'mouseout',
//   'legendselectchanged', 'datazoom', 'brush', 'brushselected',
//   'rendered', 'finished'

chart.on('click', 'series', (params) => {
  console.log('series index:', params.seriesIndex);
  console.log('data index:', params.dataIndex);
  console.log('value:', params.value);
  console.log('name:', params.name);
});

chart.on('click', { seriesType: 'pie' }, (params) => {
  // scoped handler
});

// Dispatch action programmatically
chart.dispatchAction({
  type: 'highlight',
  seriesIndex: 0,
  dataIndex: 2
});

chart.dispatchAction({
  type: 'showTip',
  seriesIndex: 0,
  dataIndex: 1
});

chart.dispatchAction({
  type: 'dataZoom',
  startValue: 10,
  endValue: 50
});
```
