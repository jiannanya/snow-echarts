# Boxplot Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-boxplot

---

## Example 1 — Basic Boxplot with Outliers

**Use case**: Compare distributions across groups; show median, quartiles, and outliers.  
**Editor**: [boxplot-light-velocity](https://echarts.apache.org/examples/en/editor.html?c=boxplot-light-velocity)

```js
// data format: [min, Q1, median, Q3, max]
const option = {
  title: { text: 'Delivery Time Distribution by Carrier', left: 'center' },
  tooltip: {
    trigger: 'item',
    axisPointer: { type: 'shadow' },
    formatter: params => {
      if (params.seriesType === 'boxplot') {
        const v = params.data;
        return `${params.name}<br/>
          Max: ${v[5]} days<br/>
          Q3: ${v[4]} days<br/>
          Median: ${v[3]} days<br/>
          Q1: ${v[2]} days<br/>
          Min: ${v[1]} days`;
      }
      return `Outlier: ${params.data[1]} days`;
    }
  },
  legend: { bottom: 10, data: ['Delivery Days', 'Outliers'] },
  grid: { left: '3%', right: '4%', bottom: '12%', containLabel: true },
  xAxis: {
    type: 'category',
    data: ['FedEx', 'UPS', 'USPS', 'DHL', 'Amazon']
  },
  yAxis: { type: 'value', name: 'Days', min: 0 },
  series: [
    {
      name: 'Delivery Days',
      type: 'boxplot',
      data: [
        [1, 2, 3, 4, 7],    // FedEx
        [2, 3, 4, 5, 8],    // UPS
        [1, 2, 3, 5, 10],   // USPS
        [1, 2, 3, 4, 6],    // DHL
        [1, 1, 2, 3, 5]     // Amazon
      ],
      itemStyle: {
        borderColor: '#5470c6',
        color: 'rgba(84,112,198,0.2)'
      }
    },
    {
      name: 'Outliers',
      type: 'scatter',
      data: [
        [2, 14],  // USPS outlier
        [0, 12],  // FedEx outlier
        [4, 11]   // Amazon outlier
      ],
      itemStyle: { color: '#ee6666' },
      symbolSize: 8
    }
  ]
};
```

---

## Example 2 — Multiple Category Boxplot

**Use case**: Compare performance distributions across years and departments.  
**Editor**: [boxplot-multi](https://echarts.apache.org/examples/en/editor.html?c=boxplot-multi)

```js
const option = {
  title: { text: 'Test Scores by Subject & Year', left: 'center' },
  tooltip: { trigger: 'axis', axisPointer: { type: 'shadow' } },
  legend: { top: 30, data: ['2022', '2023', '2024'] },
  grid: { left: '3%', right: '4%', bottom: '3%', containLabel: true },
  xAxis: {
    type: 'category',
    data: ['Math', 'Science', 'English', 'History', 'Arts']
  },
  yAxis: { type: 'value', name: 'Score', min: 50, max: 100 },
  series: [
    {
      name: '2022',
      type: 'boxplot',
      // [min, Q1, median, Q3, max]
      data: [
        [55, 65, 72, 80, 95],
        [60, 70, 75, 82, 92],
        [58, 68, 74, 82, 94],
        [50, 62, 70, 78, 90],
        [62, 72, 78, 85, 96]
      ]
    },
    {
      name: '2023',
      type: 'boxplot',
      data: [
        [58, 68, 75, 83, 97],
        [62, 72, 78, 85, 94],
        [60, 70, 76, 84, 96],
        [53, 65, 73, 81, 92],
        [65, 75, 80, 88, 98]
      ]
    },
    {
      name: '2024',
      type: 'boxplot',
      data: [
        [60, 70, 78, 86, 98],
        [64, 74, 80, 87, 96],
        [62, 72, 78, 86, 97],
        [55, 67, 75, 83, 94],
        [67, 77, 82, 90, 99]
      ]
    }
  ]
};
```

---

## Example 3 — Horizontal Boxplot (auto-computed quartiles)

**Use case**: Use raw sample data and let ECharts compute the 5-number summary.  
**Editor**: [data-transform-aggregate](https://echarts.apache.org/examples/en/editor.html?c=data-transform-aggregate)

```js
// Utility to compute boxplot stats from raw values
function computeBoxData(values) {
  const sorted = [...values].sort((a, b) => a - b);
  const n = sorted.length;
  const q1 = sorted[Math.floor(n * 0.25)];
  const median = sorted[Math.floor(n * 0.5)];
  const q3 = sorted[Math.floor(n * 0.75)];
  const iqr = q3 - q1;
  const min = Math.max(sorted[0], q1 - 1.5 * iqr);
  const max = Math.min(sorted[n - 1], q3 + 1.5 * iqr);
  const outliers = sorted.filter(v => v < min || v > max);
  return { box: [min, q1, median, q3, max], outliers };
}

const rawGroups = {
  'Group A': [45, 52, 60, 58, 63, 70, 72, 80, 55, 48, 95, 100, 62, 67],
  'Group B': [55, 60, 65, 70, 72, 75, 68, 73, 80, 85, 58, 62, 77],
  'Group C': [30, 40, 50, 55, 60, 65, 48, 52, 58, 70, 35, 110, 62]
};

const groups = Object.keys(rawGroups);
const computed = groups.map(g => computeBoxData(rawGroups[g]));

const option = {
  title: { text: 'Response Time Distribution (ms)', left: 'center' },
  tooltip: { trigger: 'item' },
  grid: { left: '3%', right: '10%', bottom: '3%', containLabel: true },
  xAxis: { type: 'value', name: 'Response Time (ms)' },
  yAxis: { type: 'category', data: groups },
  series: [
    {
      type: 'boxplot',
      data: computed.map(c => c.box),
      encode: { x: [0, 1, 2, 3, 4], y: 0 }
    },
    {
      type: 'scatter',
      data: computed.flatMap((c, i) => c.outliers.map(v => [v, i])),
      itemStyle: { color: '#ee6666' },
      symbolSize: 8
    }
  ]
};
```
