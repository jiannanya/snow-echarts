# Dataset & DataZoom Examples

> Official examples:  
> - Dataset: https://echarts.apache.org/examples/en/index.html#chart-type-dataset  
> - DataZoom: https://echarts.apache.org/examples/en/index.html#chart-type-dataZoom

---

## Dataset — Example 1: Multiple Series from One Dataset

**Use case**: Declare data once in `dataset.source` and bind multiple series via `encode`.  
**Editor**: [dataset-simple0](https://echarts.apache.org/examples/en/editor.html?c=dataset-simple0)

```js
const option = {
  title: { text: 'Product Sales by Quarter', left: 'center' },
  tooltip: { trigger: 'axis' },
  legend: { bottom: 10, data: ['Product A', 'Product B', 'Product C'] },
  dataset: {
    // First row is the header; ECharts detects it automatically
    source: [
      ['Quarter', 'Product A', 'Product B', 'Product C'],
      ['Q1 2023',  120,  80,  60],
      ['Q2 2023',  140, 110,  75],
      ['Q3 2023',  160,  95,  90],
      ['Q4 2023',  190, 130, 110],
      ['Q1 2024',  170, 120, 100],
      ['Q2 2024',  200, 145, 130]
    ]
  },
  xAxis: { type: 'category' },
  yAxis: { type: 'value', name: 'Units Sold' },
  series: [
    { type: 'bar',  name: 'Product A', encode: { x: 'Quarter', y: 'Product A' } },
    { type: 'bar',  name: 'Product B', encode: { x: 'Quarter', y: 'Product B' } },
    { type: 'line', name: 'Product C', encode: { x: 'Quarter', y: 'Product C' }, smooth: true }
  ]
};
```

---

## Dataset — Example 2: Dataset with Transform (Filter + Sort)

**Use case**: Use built-in `filter` and `sort` transforms to create derived datasets for comparison.  
**Editor**: [dataset-link](https://echarts.apache.org/examples/en/editor.html?c=dataset-link)

```js
const option = {
  title: { text: 'Top Products — Transform Demo', left: 'center' },
  tooltip: { trigger: 'item' },
  legend: { bottom: 10 },
  dataset: [
    // Raw dataset
    {
      id: 'raw',
      source: [
        { product: 'Laptop',   revenue: 450000, units: 1200, category: 'Electronics' },
        { product: 'Phone',    revenue: 380000, units: 3500, category: 'Electronics' },
        { product: 'Tablet',   revenue: 200000, units: 900,  category: 'Electronics' },
        { product: 'Desk',     revenue: 150000, units: 600,  category: 'Furniture' },
        { product: 'Chair',    revenue: 120000, units: 800,  category: 'Furniture' },
        { product: 'Monitor',  revenue: 220000, units: 1100, category: 'Electronics' }
      ]
    },
    // Filter: only Electronics
    {
      id: 'electronics',
      fromDatasetId: 'raw',
      transform: {
        type: 'filter',
        config: { dimension: 'category', value: 'Electronics' }
      }
    },
    // Sort by revenue descending
    {
      id: 'topRevenue',
      fromDatasetId: 'raw',
      transform: {
        type: 'sort',
        config: { dimension: 'revenue', order: 'desc' }
      }
    }
  ],
  grid: [
    { left: '5%',  top: 60, width: '40%', bottom: 60 },
    { right: '5%', top: 60, width: '40%', bottom: 60 }
  ],
  xAxis: [
    { gridIndex: 0, type: 'category', name: 'Electronics' },
    { gridIndex: 1, type: 'category', name: 'All Products (by Revenue)' }
  ],
  yAxis: [
    { gridIndex: 0, type: 'value', name: 'Revenue ($)' },
    { gridIndex: 1, type: 'value', name: 'Revenue ($)' }
  ],
  series: [
    {
      type: 'bar',
      name: 'Electronics',
      datasetId: 'electronics',
      xAxisIndex: 0, yAxisIndex: 0,
      encode: { x: 'product', y: 'revenue' }
    },
    {
      type: 'bar',
      name: 'All Products',
      datasetId: 'topRevenue',
      xAxisIndex: 1, yAxisIndex: 1,
      encode: { x: 'product', y: 'revenue' },
      itemStyle: { color: '#ee6666' }
    }
  ]
};
```

---

## DataZoom — Example 1: Slider + Inside DataZoom

**Use case**: Let users zoom/scroll a dense time-series chart with both a slider and wheel/pinch.  
**Editor**: [area-simple](https://echarts.apache.org/examples/en/editor.html?c=area-simple)

```js
// Generate 365 days of data
const days = [];
const values = [];
let base = 100;
for (let i = 0; i < 365; i++) {
  const d = new Date(2024, 0, i + 1);
  days.push(d.toISOString().slice(0, 10));
  base += Math.round(Math.random() * 20 - 9);
  values.push(Math.max(50, base));
}

const option = {
  title: { text: 'Daily Stock Price — DataZoom Demo', left: 'center' },
  tooltip: {
    trigger: 'axis',
    axisPointer: { type: 'cross' }
  },
  toolbox: {
    feature: {
      dataZoom: { yAxisIndex: 'none' },
      restore: {},
      saveAsImage: {}
    }
  },
  xAxis: { type: 'category', data: days, boundaryGap: false },
  yAxis: { type: 'value', name: 'Price ($)', scale: true },
  dataZoom: [
    {
      // Slider below the chart
      type: 'slider',
      start: 70,  // start visible at 70% through the data
      end: 100,
      bottom: 40,
      height: 30,
      handleIcon: 'path://M10.7,11.9v-1.3H9.3v1.3c-4.9,0.3-8.8,4.4-8.8,9.4c0,5,3.9,9.1,8.8,9.4v1.3h1.3v-1.3c4.9-0.3,8.8-4.4,8.8-9.4C19.5,16.3,15.6,12.2,10.7,11.9z M13.3,24.4H6.7V23h6.6V24.4z M13.3,19.6H6.7v-1.4h6.6V19.6z',
      handleSize: '80%'
    },
    {
      // Mouse wheel + touch zoom
      type: 'inside',
      start: 70,
      end: 100
    }
  ],
  series: [
    {
      type: 'line',
      data: values,
      smooth: 0.3,
      symbol: 'none',
      lineStyle: { width: 2 },
      areaStyle: {
        color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
          { offset: 0, color: 'rgba(84,112,198,0.7)' },
          { offset: 1, color: 'rgba(84,112,198,0.1)' }
        ])
      },
      markLine: {
        data: [{ type: 'average', name: 'Average' }]
      }
    }
  ]
};
```

---

## DataZoom — Example 2: Y-Axis DataZoom + Locked Axis

**Use case**: Zoom both X and Y axes independently to explore 2D scatter data.  
**Editor**: [scatter-weight](https://echarts.apache.org/examples/en/editor.html?c=scatter-weight)

```js
const scatterData = Array.from({ length: 200 }, () => [
  +(Math.random() * 50 + 20).toFixed(1),   // Age
  +(Math.random() * 60 + 50).toFixed(1),   // Weight (kg)
  +(Math.random() * 40 + 150).toFixed(0),  // Height (cm)
  Math.random() > 0.5 ? 'Male' : 'Female'
]);

const option = {
  title: { text: 'Body Metrics (Age, Weight, Height)', left: 'center' },
  tooltip: {
    formatter: p => `Age: ${p.data[0]}<br/>Weight: ${p.data[1]} kg<br/>Height: ${p.data[2]} cm<br/>${p.data[3]}`
  },
  legend: { bottom: 50, data: ['Male', 'Female'] },
  xAxis: { type: 'value', name: 'Age', min: 15, max: 75 },
  yAxis: { type: 'value', name: 'Weight (kg)', min: 40, max: 120 },
  dataZoom: [
    { type: 'slider', xAxisIndex: 0, bottom: 20 },     // X slider
    { type: 'slider', yAxisIndex: 0, right: 20 },      // Y slider (vertical)
    { type: 'inside', xAxisIndex: 0 },
    { type: 'inside', yAxisIndex: 0 }
  ],
  series: [
    {
      name: 'Male',
      type: 'scatter',
      symbolSize: p => Math.max(6, (p[2] - 150) * 0.3 + 6),
      data: scatterData.filter(d => d[3] === 'Male')
    },
    {
      name: 'Female',
      type: 'scatter',
      symbolSize: p => Math.max(6, (p[2] - 150) * 0.3 + 6),
      data: scatterData.filter(d => d[3] === 'Female'),
      itemStyle: { opacity: 0.7 }
    }
  ]
};
```
