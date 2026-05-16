# 3D / GL Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-bar3D  
> **Requires [echarts-gl](https://github.com/ecomfe/echarts-gl)**  
> Install: `npm install echarts-gl` — then `import 'echarts-gl'` alongside `echarts`.

---

## Example 1 — 3D Bar Chart (bar3D)

**Use case**: Compare a 2D grid of values across two category axes using vertical bars.  
**Editor**: [bar3d-with-surface](https://echarts.apache.org/examples/en/editor.html?c=bar3d-with-surface)

```js
// Requires echarts-gl
const months  = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
const regions = ['North', 'South', 'East', 'West', 'Central'];

const data = [];
regions.forEach((region, ri) => {
  months.forEach((month, mi) => {
    data.push([mi, ri, Math.round(Math.random() * 100 + 20)]);
  });
});

const option = {
  title: { text: 'Monthly Sales by Region (3D Bar)', left: 'center' },
  tooltip: {},
  visualMap: {
    max: 120,
    inRange: { color: ['#313695', '#4575b4', '#74add1', '#ffffbf', '#f46d43', '#a50026'] }
  },
  xAxis3D: { type: 'category', data: months, name: 'Month' },
  yAxis3D: { type: 'category', data: regions, name: 'Region' },
  zAxis3D: { type: 'value', name: 'Sales' },
  grid3D: {
    boxWidth: 200,
    boxDepth: 80,
    viewControl: {
      // Initial rotation angle
      beta: 30,
      alpha: 20
    },
    light: {
      main: { intensity: 1.2 },
      ambient: { intensity: 0.3 }
    }
  },
  series: [
    {
      type: 'bar3D',
      data: data,
      shading: 'color',
      label: { show: false },
      itemStyle: { opacity: 0.8 },
      emphasis: {
        label: { show: true, textStyle: { fontSize: 16, color: '#900' } },
        itemStyle: { color: '#900' }
      }
    }
  ]
};
```

---

## Example 2 — 3D Scatter Chart (scatter3D)

**Use case**: Visualize three-dimensional correlations in a dataset — e.g., health metrics.  
**Editor**: [scatter3d](https://echarts.apache.org/examples/en/editor.html?c=scatter3d)

```js
// Requires echarts-gl
const data = Array.from({ length: 300 }, () => {
  const age    = Math.random() * 50 + 20;               // 20-70
  const bmi    = Math.random() * 20 + 18;               // 18-38
  const sleep  = Math.random() * 4 + 4;                 // 4-8 hrs
  // Rough risk score (higher is more risk)
  const risk   = (age / 70 * 0.4 + bmi / 38 * 0.4 + (8 - sleep) / 4 * 0.2) * 100;
  return [+age.toFixed(1), +bmi.toFixed(1), +sleep.toFixed(1), +risk.toFixed(1)];
});

const option = {
  title: { text: 'Health Risk 3D Scatter (Age × BMI × Sleep)', left: 'center' },
  tooltip: {
    formatter: p => `Age: ${p.data[0]}<br/>BMI: ${p.data[1]}<br/>Sleep: ${p.data[2]} hrs<br/>Risk: ${p.data[3]}%`
  },
  visualMap: {
    max: 100,
    dimension: 3,
    inRange: { color: ['#2ecc71', '#f1c40f', '#e74c3c'] },
    orient: 'vertical',
    right: 20,
    top: 'middle'
  },
  xAxis3D: { type: 'value', name: 'Age' },
  yAxis3D: { type: 'value', name: 'BMI' },
  zAxis3D: { type: 'value', name: 'Sleep (hrs)' },
  grid3D: {
    viewControl: { beta: 40, alpha: 15 }
  },
  series: [
    {
      type: 'scatter3D',
      data: data,
      symbolSize: 6,
      itemStyle: { opacity: 0.7 },
      emphasis: { itemStyle: { opacity: 1 } }
    }
  ]
};
```

---

## Example 3 — 3D Globe with Flight Routes (Lines3D)

**Use case**: Render geographic paths or connections on a spinning globe.  
**Editor**: [globe-airline](https://echarts.apache.org/examples/en/editor.html?c=globe-airline)

```js
// Requires echarts-gl
// Airport coordinates: [longitude, latitude]
const airports = {
  'New York':    [-74.006, 40.713],
  'London':      [-0.128, 51.508],
  'Tokyo':       [139.692, 35.689],
  'Dubai':       [55.270, 25.204],
  'Singapore':   [103.820, 1.352],
  'Sydney':      [151.209, -33.868],
  'São Paulo':   [-46.634, -23.548],
  'Los Angeles': [-118.243, 34.052],
  'Paris':       [2.350, 48.853],
  'Mumbai':      [72.877, 19.076]
};

const routes = [
  ['New York', 'London'],
  ['New York', 'Tokyo'],
  ['New York', 'Dubai'],
  ['London', 'Dubai'],
  ['London', 'Singapore'],
  ['Dubai', 'Singapore'],
  ['Dubai', 'Mumbai'],
  ['Singapore', 'Sydney'],
  ['Tokyo', 'Los Angeles'],
  ['Los Angeles', 'New York'],
  ['São Paulo', 'New York'],
  ['São Paulo', 'London'],
  ['Paris', 'Dubai'],
  ['Paris', 'New York']
];

const lineData = routes.map(([from, to]) => ({
  coords: [airports[from], airports[to]]
}));

const pointData = Object.entries(airports).map(([name, coords]) => ({
  name,
  value: [...coords, Math.floor(Math.random() * 100 + 50)] // traffic volume
}));

const option = {
  globe: {
    baseTexture: 'https://echarts.apache.org/examples/data-gl/asset/world.topo.bathy.200401.jpg',
    heightTexture: 'https://echarts.apache.org/examples/data-gl/asset/bathymetry_bw_composite_4k.jpg',
    shading: 'realistic',
    light: { ambient: { intensity: 0.4 }, main: { intensity: 1 } },
    atmosphere: { show: true },
    viewControl: { autoRotate: true, autoRotateSpeed: 8 }
  },
  series: [
    {
      type: 'lines3D',
      coordinateSystem: 'globe',
      lineStyle: { color: '#ffa500', width: 1.5, opacity: 0.5 },
      effect: {
        show: true,
        period: 4,
        trailLength: 0.3,
        color: '#fff',
        symbolSize: 4
      },
      blendMode: 'lighter',
      data: lineData
    },
    {
      type: 'scatter3D',
      coordinateSystem: 'globe',
      symbol: 'circle',
      symbolSize: 8,
      itemStyle: { color: '#ff6b35', opacity: 1 },
      label: {
        show: true,
        formatter: '{b}',
        fontSize: 10,
        color: '#fff',
        distance: 8
      },
      data: pointData
    }
  ]
};
```
