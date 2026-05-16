# Scatter Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-scatter

---

## Example 1 — Bubble Chart (3D scatter with size encoding)

**Use case**: Three-variable scatter — x, y position + bubble size for a third dimension.  
**Editor**: [scatter-simple](https://echarts.apache.org/examples/en/editor.html?c=scatter-simple)

```js
const option = {
  title: { text: 'GDP vs Life Expectancy (2022)', left: 'center' },
  tooltip: {
    trigger: 'item',
    formatter: params => {
      const [country, gdp, lifeExp, population] = params.data;
      return `<b>${country}</b><br/>
        GDP per capita: $${gdp.toLocaleString()}<br/>
        Life Expectancy: ${lifeExp} yrs<br/>
        Population: ${(population / 1e6).toFixed(0)}M`;
    }
  },
  legend: { bottom: 10, data: ['Asia', 'Europe', 'Americas', 'Africa'] },
  grid: { left: '3%', right: '3%', bottom: '12%', containLabel: true },
  xAxis: {
    name: 'GDP per Capita ($)',
    type: 'log',
    min: 300,
    max: 100000,
    axisLabel: { formatter: val => `$${(val / 1000).toFixed(0)}k` }
  },
  yAxis: {
    name: 'Life Expectancy (yrs)',
    min: 40,
    max: 90
  },
  series: [
    {
      name: 'Asia',
      type: 'scatter',
      symbolSize: d => Math.sqrt(d[3]) / 500,
      data: [
        ['China', 13720, 77.5, 1412000000],
        ['India', 2300, 69.4, 1380000000],
        ['Japan', 33815, 84.3, 125000000],
        ['Indonesia', 4691, 71.7, 273000000],
        ['South Korea', 33591, 83.5, 51000000]
      ],
      itemStyle: { opacity: 0.7 }
    },
    {
      name: 'Europe',
      type: 'scatter',
      symbolSize: d => Math.sqrt(d[3]) / 500,
      data: [
        ['Germany', 46253, 81.1, 83000000],
        ['France', 42330, 82.5, 67000000],
        ['UK', 42300, 81.4, 67000000],
        ['Italy', 33228, 83.4, 60000000],
        ['Spain', 29600, 83.6, 47000000]
      ],
      itemStyle: { opacity: 0.7 }
    },
    {
      name: 'Americas',
      type: 'scatter',
      symbolSize: d => Math.sqrt(d[3]) / 500,
      data: [
        ['USA', 63543, 79.1, 331000000],
        ['Canada', 46195, 82.9, 38000000],
        ['Brazil', 8717, 75.9, 215000000],
        ['Mexico', 10276, 75.0, 130000000]
      ],
      itemStyle: { opacity: 0.7 }
    },
    {
      name: 'Africa',
      type: 'scatter',
      symbolSize: d => Math.sqrt(d[3]) / 500,
      data: [
        ['Nigeria', 2237, 54.7, 216000000],
        ['Ethiopia', 950, 67.8, 120000000],
        ['South Africa', 6994, 62.3, 60000000],
        ['Kenya', 2061, 67.5, 55000000]
      ],
      itemStyle: { opacity: 0.7 }
    }
  ]
};
```

---

## Example 2 — Effect Scatter with ripple (geographic hotspots)

**Use case**: Highlight important data points with animated ripple effects.  
**Editor**: [scatter-effect](https://echarts.apache.org/examples/en/editor.html?c=scatter-effect)

```js
const option = {
  title: { text: 'Top Sales Offices — Performance Score', left: 'center' },
  tooltip: {
    trigger: 'item',
    formatter: p => `${p.data[2]}: Score ${p.data[3]}`
  },
  xAxis: { type: 'value', name: 'Revenue ($M)', min: 0, max: 50 },
  yAxis: { type: 'value', name: 'Customer Satisfaction', min: 0, max: 100 },
  visualMap: {
    min: 0, max: 100,
    dimension: 3,
    orient: 'vertical',
    right: 10,
    top: 'center',
    inRange: {
      color: ['#65B581', '#FFCE34', '#FD665F']
    }
  },
  series: [
    {
      type: 'scatter',
      symbolSize: 15,
      data: [
        [12, 78, 'Boston', 82],
        [22, 65, 'Chicago', 67],
        [8, 90, 'Austin', 91],
        [35, 55, 'Dallas', 55],
        [18, 82, 'Seattle', 84],
        [42, 48, 'Miami', 48],
        [28, 71, 'Denver', 72],
        [15, 88, 'Portland', 89]
      ],
      itemStyle: { opacity: 0.6 }
    },
    {
      // Highlight top performers with ripple effect
      type: 'effectScatter',
      symbolSize: 20,
      rippleEffect: { brushType: 'stroke', scale: 3 },
      data: [
        [8, 90, 'Austin', 91],
        [15, 88, 'Portland', 89],
        [18, 82, 'Seattle', 84]
      ],
      label: {
        show: true,
        formatter: p => p.data[2],
        position: 'right'
      }
    }
  ]
};
```

---

## Example 3 — Scatter with Regression Line (custom series overlay)

**Use case**: Show correlation between two variables with a trend line.  
**Editor**: [scatter-linear-regression](https://echarts.apache.org/examples/en/editor.html?c=scatter-linear-regression)

```js
// Linear regression helper
function linearRegression(data) {
  const n = data.length;
  let sumX = 0, sumY = 0, sumXY = 0, sumX2 = 0;
  data.forEach(([x, y]) => { sumX += x; sumY += y; sumXY += x * y; sumX2 += x * x; });
  const slope = (n * sumXY - sumX * sumY) / (n * sumX2 - sumX * sumX);
  const intercept = (sumY - slope * sumX) / n;
  return { slope, intercept };
}

const rawData = [
  [10, 8.04], [8, 6.95], [13, 7.58], [9, 8.81], [11, 8.33],
  [14, 9.96], [6, 7.24], [4, 4.26], [12, 10.84], [7, 4.82], [5, 5.68]
];
const { slope, intercept } = linearRegression(rawData);
const xMin = Math.min(...rawData.map(d => d[0]));
const xMax = Math.max(...rawData.map(d => d[0]));

const option = {
  title: { text: 'Scatter with Linear Regression', left: 'center' },
  tooltip: {
    trigger: 'axis',
    axisPointer: { type: 'cross' }
  },
  xAxis: { name: 'X', min: xMin - 1, max: xMax + 1 },
  yAxis: { name: 'Y' },
  series: [
    {
      name: 'Observations',
      type: 'scatter',
      symbolSize: 10,
      data: rawData,
      label: {
        show: false
      }
    },
    {
      name: `Trend (y = ${slope.toFixed(2)}x + ${intercept.toFixed(2)})`,
      type: 'line',
      data: [[xMin, slope * xMin + intercept], [xMax, slope * xMax + intercept]],
      lineStyle: { color: '#ee6666', type: 'dashed', width: 2 },
      symbol: 'none',
      tooltip: { show: false }
    }
  ]
};
```
