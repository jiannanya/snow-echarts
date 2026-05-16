# Parallel Coordinates Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-parallel

---

## Example 1 — Parallel Coordinates for AQI Data

**Use case**: Compare multi-dimensional environmental data across cities.  
**Editor**: [parallel-aqi](https://echarts.apache.org/examples/en/editor.html?c=parallel-aqi)

```js
const schema = [
  { name: 'City' },
  { name: 'PM2.5', max: 250 },
  { name: 'PM10',  max: 400 },
  { name: 'CO',    max: 5 },
  { name: 'NO₂',  max: 150 },
  { name: 'SO₂',  max: 100 },
  { name: 'O₃',   max: 200 },
  { name: 'AQI',  max: 300 }
];

// [City, PM2.5, PM10, CO, NO2, SO2, O3, AQI]
const data = [
  ['Beijing',      85, 130, 1.8, 80, 40, 100, 120],
  ['Shanghai',     60, 95,  1.2, 60, 25, 110,  90],
  ['Tokyo',        20, 40,  0.5, 30, 10, 130,  45],
  ['Los Angeles',  30, 60,  0.6, 50, 10, 120,  60],
  ['London',       18, 40,  0.4, 35, 15,  90,  40],
  ['Paris',        22, 45,  0.5, 40, 18,  95,  48],
  ['Delhi',       150, 220, 3.2,120, 70,  80, 200],
  ['Mumbai',       90, 140, 2.0, 90, 50,  90, 130],
  ['Sydney',       10, 20,  0.3, 20,  5, 140,  25],
  ['New York',     28, 55,  0.5, 45, 15, 115,  55]
];

const option = {
  title: { text: 'City Air Quality Index — Parallel Coordinates', left: 'center' },
  tooltip: {
    trigger: 'item',
    formatter: params => schema.slice(1)
      .map((s, i) => `${s.name}: ${params.data[i + 1]}`)
      .join('<br/>')
  },
  parallelAxis: schema.slice(1).map((s, i) => ({
    dim: i,
    name: s.name,
    max: s.max,
    nameTextStyle: { fontSize: 11 }
  })),
  parallel: {
    left: '5%',
    right: '5%',
    top: 80,
    bottom: 60,
    parallelAxisDefault: {
      type: 'value',
      nameLocation: 'end',
      nameGap: 20
    }
  },
  visualMap: {
    show: true,
    min: 0,
    max: 300,
    dimension: 6,   // color by AQI
    orient: 'horizontal',
    left: 'center',
    bottom: 5,
    inRange: { color: ['#66bb6a', '#ffa726', '#ef5350'] }
  },
  series: [
    {
      type: 'parallel',
      lineStyle: { width: 1.5, opacity: 0.6 },
      data: data.map(row => row.slice(1))  // exclude city name
    }
  ]
};
```

---

## Example 2 — Cars Dataset (Parallel with Brush)

**Use case**: Explore multi-attribute data with interactive axis brushing to filter.  
**Editor**: [parallel-nutrients](https://echarts.apache.org/examples/en/editor.html?c=parallel-nutrients)

```js
// Car attributes: [mpg, cylinders, displacement, horsepower, weight, acceleration, year]
const cars = [
  [18, 8, 307, 130, 3504, 12, 70],
  [15, 8, 350, 165, 3693, 11.5, 70],
  [18, 8, 318, 150, 3436, 11, 70],
  [16, 8, 304, 150, 3433, 12, 70],
  [17, 8, 302, 140, 3449, 10.5, 70],
  [30, 4, 97,  88, 2130, 14.5, 71],
  [28, 4, 107, 90, 2130, 14.5, 71],
  [35, 4, 113, 95, 2228, 14, 71],
  [27, 4, 97,  88, 2130, 14.5, 71],
  [26, 4, 97,  88, 2130, 14.5, 71],
  [25, 4, 110, 87, 2672, 17.5, 70],
  [24, 4, 107, 90, 2430, 14.5, 70],
  [38, 4, 91,  67, 1850, 13.8, 80],
  [41, 4, 85,  65, 2110, 19.2, 80],
  [36, 4, 98,  65, 2045, 16.2, 82]
];

const option = {
  title: { text: 'Automobile Attributes — Parallel Coordinates', left: 'center' },
  parallelAxis: [
    { dim: 0, name: 'MPG',          min: 10, max: 45 },
    { dim: 1, name: 'Cylinders',    min: 4,  max: 8,  type: 'category', data: ['4','6','8'] },
    { dim: 2, name: 'Displacement', min: 70, max: 450 },
    { dim: 3, name: 'Horsepower',   min: 50, max: 200 },
    { dim: 4, name: 'Weight (lbs)', min: 1600, max: 4000 },
    { dim: 5, name: 'Accel.',       min: 8,  max: 25 },
    { dim: 6, name: 'Year',         min: 70, max: 82 }
  ],
  parallel: {
    left: '5%', right: '5%', top: 80, bottom: 80,
    parallelAxisDefault: { nameTextStyle: { fontSize: 11 } }
  },
  brush: {},
  toolbox: {
    feature: {
      brush: { type: ['lineX', 'clear'] }
    }
  },
  visualMap: {
    show: true, dimension: 0, min: 10, max: 45,
    orient: 'horizontal', left: 'center', bottom: 20,
    inRange: { color: ['#ee6666', '#fac858', '#91cc75'] },
    text: ['High MPG', 'Low MPG']
  },
  series: [
    {
      type: 'parallel',
      lineStyle: { width: 1, opacity: 0.7 },
      data: cars
    }
  ]
};
```

---

## Example 3 — Parallel Coordinates for Stock Portfolio

**Use case**: Compare portfolio stocks on multiple financial metrics simultaneously.  
**Editor**: [parallel-simple](https://echarts.apache.org/examples/en/editor.html?c=parallel-simple)

```js
// Columns: [Ticker, P/E, P/B, EPS Growth, Dividend Yield, MarketCap($B), Beta, YTD Return]
const stocks = [
  ['AAPL',  28.5, 45.2,  12.3, 0.5,  2800, 1.20,  18.5],
  ['MSFT',  32.1, 13.8,  15.6, 0.9,  2600, 0.90,  22.1],
  ['GOOGL', 24.3,  5.9,  18.2, 0.0,  1700, 1.05,  15.3],
  ['AMZN',  58.4,  9.2,  28.5, 0.0,  1500, 1.15,  10.2],
  ['META',  22.1, 6.8,   22.1, 0.4,   900, 1.25,  35.4],
  ['JNJ',   16.8, 5.1,   3.2,  2.8,   450, 0.55,   2.1],
  ['KO',    24.5, 10.5,  2.8,  3.1,   260, 0.60,   3.5],
  ['PG',    26.3,  8.2,  4.1,  2.5,   350, 0.60,   4.8],
  ['XOM',   12.5,  2.1,  8.8,  3.5,   450, 0.80,  -8.5],
  ['JPM',   11.2,  1.8,  12.3, 2.4,   500, 1.10,  12.3]
];

const option = {
  title: { text: 'Stock Portfolio Comparison', left: 'center' },
  parallelAxis: [
    { dim: 0, type: 'category', data: stocks.map(s => s[0]), name: 'Ticker' },
    { dim: 1, name: 'P/E',       min: 10, max: 65 },
    { dim: 2, name: 'P/B',       min: 1,  max: 50 },
    { dim: 3, name: 'EPS Growth', min: 0, max: 30 },
    { dim: 4, name: 'Div Yield', min: 0, max: 4 },
    { dim: 5, name: 'Mkt Cap ($B)', min: 200, max: 3000 },
    { dim: 6, name: 'Beta',      min: 0.4, max: 1.4 },
    { dim: 7, name: 'YTD Return %', min: -15, max: 40 }
  ],
  parallel: { left: '5%', right: '5%', top: 80, bottom: 80 },
  visualMap: {
    show: true, dimension: 7, min: -15, max: 40,
    orient: 'horizontal', left: 'center', bottom: 20,
    inRange: { color: ['#d73027', '#ffffbf', '#1a9850'] },
    text: ['+40%', '-15%']
  },
  series: [
    {
      type: 'parallel',
      lineStyle: { width: 2, opacity: 0.7 },
      data: stocks.map(s => s.slice(1))
    }
  ]
};
```
