# ECharts Chart Types Reference

All chart types are set via `series[i].type`. Most cartesian charts require `xAxis` + `yAxis` + `grid`.

---

## Cartesian Charts (require xAxis + yAxis)

### `bar` — Bar / Column Chart
```js
series: [{
  type: 'bar',
  name: 'Sales',
  data: [120, 200, 150, 80, 70],
  // Key options:
  barWidth: '40%',          // bar width (px or %)
  barMaxWidth: 60,
  barGap: '30%',            // gap between bars in same category
  barCategoryGap: '20%',    // gap between category groups
  stack: 'total',           // stacked bar key (same key = stacked)
  label: { show: true, position: 'top' },
  itemStyle: { color: '#5470c6', borderRadius: [4, 4, 0, 0] },
  emphasis: { itemStyle: { color: '#264fc5' } }
}]
```
- **Horizontal bar**: swap `xAxis.type = 'value'` and `yAxis.type = 'category'`
- **Stacked**: multiple series with same `stack` value

### `line` — Line Chart
```js
series: [{
  type: 'line',
  name: 'Trend',
  data: [820, 932, 901, 934, 1290],
  // Key options:
  smooth: true,             // smooth curve (or 0–1 smoothness)
  step: false,              // 'start'|'middle'|'end' for step lines
  lineStyle: { width: 2, type: 'solid' },  // 'dashed'|'dotted'
  areaStyle: { opacity: 0.3 },             // fill area under line
  symbol: 'circle',         // 'circle'|'rect'|'diamond'|'none'
  symbolSize: 8,
  stack: 'total',           // stacked area chart
  connectNulls: true,
  markPoint: { data: [{ type: 'max', name: 'Max' }] },
  markLine: { data: [{ type: 'average', name: 'Avg' }] }
}]
```

### `scatter` — Scatter Plot
```js
series: [{
  type: 'scatter',
  data: [[10, 20], [30, 40], [50, 10]],  // [x, y] or [x, y, size, ...]
  // Key options:
  symbolSize: (data) => data[2] * 2,    // size by third value
  itemStyle: { opacity: 0.7 },
  large: true,              // enable for >10k points
  largeThreshold: 2000
}]
```

### `effectScatter` — Animated Scatter (ripple effect)
```js
series: [{
  type: 'effectScatter',
  data: [[10, 20], [30, 40]],
  symbolSize: 20,
  rippleEffect: { brushType: 'stroke', scale: 3, period: 4 },
  showEffectOn: 'render'   // 'render'|'emphasis'
}]
```

### `boxplot` — Box Plot
```js
// data: [min, Q1, median, Q3, max]
series: [{
  type: 'boxplot',
  data: [[655, 850, 940, 980, 1175], [672, 850, 913, 987, 1250]]
}]
```

### `candlestick` — OHLC / Candlestick
```js
// data: [open, close, low, high]
series: [{
  type: 'candlestick',
  data: [[20, 34, 10, 38], [40, 35, 30, 50]],
  itemStyle: {
    color: '#ec0000',       // bullish (up) color
    color0: '#00da3c',      // bearish (down) color
    borderColor: '#8A0000',
    borderColor0: '#008F28'
  }
}]
```

### `heatmap` — Heatmap (on grid)
```js
// Requires visualMap component
xAxis: { type: 'category', data: hours },
yAxis: { type: 'category', data: days },
visualMap: { min: 0, max: 10, calculable: true },
series: [{
  type: 'heatmap',
  data: [[0, 0, 5], [0, 1, 1], [1, 0, 8]],  // [xIndex, yIndex, value]
  label: { show: true }
}]
```

### `pictorialBar` — Pictorial Bar
```js
series: [{
  type: 'pictorialBar',
  data: [120, 200, 150],
  symbol: 'path://M0,10 L10,0 L20,10 Z',  // custom SVG path or built-in symbol
  symbolSize: ['80%', '100%'],
  symbolRepeat: true
}]
```

---

## Circular / Non-Cartesian Charts

### `pie` — Pie / Donut Chart
```js
series: [{
  type: 'pie',
  name: 'Browser Share',
  data: [
    { value: 1048, name: 'Chrome' },
    { value: 735, name: 'Firefox' },
    { value: 580, name: 'Edge' }
  ],
  // Key options:
  radius: ['40%', '70%'],  // [inner, outer] → donut. '70%' → full pie
  center: ['50%', '50%'],
  roseType: 'radius',      // Nightingale rose: 'radius'|'area'
  label: { show: true, formatter: '{b}: {d}%' },
  emphasis: {
    itemStyle: { shadowBlur: 10, shadowColor: 'rgba(0,0,0,0.5)' },
    label: { show: true, fontSize: 14, fontWeight: 'bold' }
  },
  padAngle: 3,             // gap between slices (degrees)
  startAngle: 90
}]
```

### `radar` — Radar / Spider Chart
```js
radar: {
  indicator: [
    { name: 'Sales', max: 6500 },
    { name: 'Admin', max: 16000 },
    { name: 'IT', max: 30000 }
  ],
  shape: 'circle'  // 'polygon'|'circle'
},
series: [{
  type: 'radar',
  data: [{
    value: [4200, 3000, 20000],
    name: 'Budget Allocation'
  }],
  areaStyle: {}
}]
```

### `gauge` — Gauge / Speedometer
```js
series: [{
  type: 'gauge',
  data: [{ value: 50, name: 'Score' }],
  // Key options:
  min: 0, max: 100,
  startAngle: 225, endAngle: -45,
  radius: '75%',
  progress: { show: true, width: 18 },
  axisLine: { lineStyle: { width: 18 } },
  pointer: { show: true },
  detail: { formatter: '{value}%', fontSize: 24 }
}]
```

### `funnel` — Funnel Chart
```js
series: [{
  type: 'funnel',
  data: [
    { value: 60, name: 'Visit' },
    { value: 40, name: 'Inquiry' },
    { value: 20, name: 'Order' },
    { value: 10, name: 'Purchase' }
  ],
  left: '10%', width: '80%',
  sort: 'descending',
  label: { show: true, position: 'inside' }
}]
```

---

## Hierarchical / Relational Charts

### `tree` — Tree Diagram
```js
series: [{
  type: 'tree',
  data: [{
    name: 'Root',
    children: [
      { name: 'Child A', children: [{ name: 'Leaf' }] },
      { name: 'Child B' }
    ]
  }],
  orient: 'LR',   // 'LR'|'RL'|'TB'|'BT'
  layout: 'orthogonal',  // 'orthogonal'|'radial'
  expandAndCollapse: true
}]
```

### `treemap` — Treemap
```js
series: [{
  type: 'treemap',
  data: [
    { name: 'A', value: 40, children: [{ name: 'A1', value: 20 }] },
    { name: 'B', value: 60 }
  ],
  roam: true,
  label: { show: true, formatter: '{b}: {c}' }
}]
```

### `sunburst` — Sunburst (multilevel pie)
```js
series: [{
  type: 'sunburst',
  data: [
    { name: 'Grandpa', value: 40, children: [
      { name: 'Uncle Leo', value: 15, children: [
        { name: 'Cousin Jack', value: 2 }
      ]}
    ]}
  ],
  radius: [0, '90%'],
  label: { rotate: 'radial' }
}]
```

### `sankey` — Sankey Diagram (flow)
```js
series: [{
  type: 'sankey',
  nodes: [{ name: 'A' }, { name: 'B' }, { name: 'C' }],
  links: [
    { source: 'A', target: 'B', value: 5 },
    { source: 'A', target: 'C', value: 3 }
  ],
  orient: 'horizontal',
  label: { show: true }
}]
```

### `graph` — Network Graph
```js
series: [{
  type: 'graph',
  layout: 'force',   // 'none'|'circular'|'force'
  nodes: [
    { id: '0', name: 'Node A', symbolSize: 30, category: 0 },
    { id: '1', name: 'Node B', symbolSize: 20, category: 1 }
  ],
  links: [{ source: '0', target: '1' }],
  categories: [{ name: 'Type A' }, { name: 'Type B' }],
  force: { repulsion: 100, edgeLength: 50 },
  roam: true,
  label: { show: true }
}]
```

---

## Geographic Charts (require `geo` or built-in)

### `map` — Choropleth Map
```js
// Register map first: echarts.registerMap('china', geoJSON)
geo: {
  map: 'china',
  roam: true,
  itemStyle: { areaColor: '#e7dfe6', borderColor: '#aaa' }
},
series: [{
  type: 'map',
  map: 'china',
  data: [{ name: 'Beijing', value: 199 }, { name: 'Shanghai', value: 155 }],
  geoIndex: 0
}]
```

### `lines` — Lines on Map (flow map)
```js
series: [{
  type: 'lines',
  coordinateSystem: 'geo',
  data: [{
    coords: [[116.4, 39.9], [121.4, 31.2]],
    lineStyle: { width: 1, color: '#ff4500' }
  }],
  effect: { show: true, symbol: 'arrow', symbolSize: 6 }
}]
```

---

## Time-Based Charts

### `themeRiver` — Theme River
```js
singleAxis: { type: 'time', boundaryGap: ['10%', '10%'] },
series: [{
  type: 'themeRiver',
  data: [
    ['2021-01-01', 20, 'Series A'],
    ['2021-01-02', 30, 'Series A'],
    ['2021-01-01', 15, 'Series B']
  ]
}]
```

### Calendar Heatmap
```js
calendar: {
  range: '2021',
  cellSize: [14, 14]
},
series: [{
  type: 'heatmap',
  coordinateSystem: 'calendar',
  data: [['2021-01-01', 10], ['2021-01-02', 5]]
}]
```

---

## Custom / Advanced

### `custom` — Fully Custom Rendering
```js
series: [{
  type: 'custom',
  renderItem: (params, api) => {
    const [x, y] = api.coord([api.value(0), api.value(1)]);
    return {
      type: 'circle',
      shape: { cx: x, cy: y, r: 20 },
      style: api.style({ fill: api.visual('color') })
    };
  },
  data: [[10, 20], [30, 40]]
}]
```

---

## Polar Coordinate Charts

### Bar on Polar
```js
polar: { radius: [30, '80%'] },
angleAxis: { max: 4, startAngle: 75 },
radiusAxis: { type: 'category', data: ['a', 'b', 'c', 'd'] },
series: [{
  type: 'bar',
  data: [2, 1.2, 2.4, 3.6],
  coordinateSystem: 'polar',
  label: { show: true, position: 'middle' }
}]
```


---

## Multi-Dimensional Charts

### `parallel` ? Parallel Coordinates

Used for exploring correlations and patterns across many numerical dimensions simultaneously.

```js
option = {
  parallelAxis: [
    { dim: 0, name: 'Price' },
    { dim: 1, name: 'Weight' },
    { dim: 2, name: 'Calories' },
    { dim: 3, name: 'Rating', max: 5 }
  ],
  parallel: {
    left: '5%', right: '13%',
    parallelAxisDefault: { type: 'value', nameLocation: 'end', nameGap: 20 }
  },
  series: [{
    type: 'parallel',
    lineStyle: { width: 2, opacity: 0.5 },
    data: [
      [12.5, 250, 320, 4.5],
      [8.0,  180, 210, 3.8],
      [15.0, 310, 450, 4.2],
      [6.5,  140, 180, 3.5]
    ]
  }]
};
```

Key options:
- `parallelAxis[n].dim` ? 0-based dimension index (required)
- `parallelAxis[n].type` ? `'value'` (numeric) or `'category'`
- `parallel.parallelAxisDefault` ? shared defaults for all axes
- Combine with `visualMap.dimension` to colour lines by a specific axis

---

## New in v6.0.0+

### `matrix` ? Matrix / Grid Chart *(v6.0.0+)*

Renders data on a matrix coordinate system (rows ? columns).  
Best for correlation matrices, schedule grids, and heat-table hybrids.

```js
option = {
  // Register the matrix coordinate system
  matrix: [{
    rowLabels: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri'],
    columnLabels: ['Morning', 'Afternoon', 'Evening']
  }],
  visualMap: {
    min: 0, max: 100,
    inRange: { color: ['#e0f3f8', '#4575b4'] }
  },
  series: [{
    type: 'heatmap',
    coordinateSystem: 'matrix',
    // data: [rowIndex, colIndex, value]
    data: [
      [0, 0, 30], [0, 1, 60], [0, 2, 80],
      [1, 0, 20], [1, 1, 75], [1, 2, 90],
      [2, 0, 50], [2, 1, 40], [2, 2, 65],
      [3, 0, 70], [3, 1, 55], [3, 2, 45],
      [4, 0, 85], [4, 1, 30], [4, 2, 25]
    ],
    label: { show: true }
  }]
};
```

Other series types that work with `coordinateSystem: 'matrix'`:
- `scatter`, `bar`, `boxplot` ? one glyph per cell

---

### `chord` ? Chord Diagram *(v6.0.0+)*

Displays flows or relationships between a set of entities arranged in a circle.

```js
option = {
  series: [{
    type: 'chord',
    radius: '65%',
    padAngle: 0.03,
    itemStyle: { borderWidth: 1, borderColor: '#fff' },
    label: { show: true, fontSize: 12 },
    // Node sizes are proportional to their total flow
    data: [
      { name: 'A', value: 100 },
      { name: 'B', value: 80  },
      { name: 'C', value: 90  },
      { name: 'D', value: 70  }
    ],
    // links define directed flows; value = magnitude
    links: [
      { source: 'A', target: 'B', value: 30 },
      { source: 'A', target: 'C', value: 25 },
      { source: 'B', target: 'D', value: 20 },
      { source: 'C', target: 'D', value: 35 },
      { source: 'D', target: 'A', value: 15 }
    ],
    // Optional: gradient edges
    lineStyle: { color: 'source', opacity: 0.6 }
  }]
};
```

Key options:
- `data[].value` ? arc size on the outer ring
- `links[].value` ? ribbon width
- `padAngle` ? gap between arcs (radians)
- `lineStyle.color: 'source'` ? ribbon inherits source-node color

---

## 3D Charts *(requires echarts-gl)*

> Add `<script src="https://cdn.jsdelivr.net/npm/echarts-gl/dist/echarts-gl.min.js"></script>`
> after the base ECharts script to unlock all 3D types.

| Series type | Description |
|---|---|
| `bar3D` | 3D bar chart on `grid3D` or `globe` |
| `scatter3D` | 3D scatter plot on `grid3D` |
| `line3D` | 3D line chart on `grid3D` |
| `surface` | Math surface / parametric surface |
| `lines3D` | Flow lines on `globe` |
| `map3D` | Extruded 3D map |
| `scatterGL` | GPU-accelerated 2D scatter |
| `linesGL` | GPU-accelerated 2D lines |
| `flowGL` | GPU-accelerated flow field |
| `graphGL` | GPU-accelerated network graph |

```js
// Minimal 3D scatter example (echarts-gl required)
option = {
  grid3D: {},
  xAxis3D: {}, yAxis3D: {}, zAxis3D: {},
  series: [{
    type: 'scatter3D',
    symbolSize: 6,
    data: Array.from({ length: 100 }, () => [
      Math.random() * 10,
      Math.random() * 10,
      Math.random() * 10
    ])
  }]
};
```
