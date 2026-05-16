# Heatmap Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-heatmap

---

## Example 1 — Hour × Day Commit Activity Heatmap

**Use case**: Show activity density across a two-dimensional grid (time of day vs. day of week).  
**Editor**: [heatmap-cartesian](https://echarts.apache.org/examples/en/editor.html?c=heatmap-cartesian)

```js
const hours = Array.from({ length: 24 }, (_, i) => `${i}:00`);
const days  = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];

// Generate random commit data [hour, day, count]
function generateData() {
  const data = [];
  for (let h = 0; h < 24; h++) {
    for (let d = 0; d < 7; d++) {
      const isWorkDay  = d >= 1 && d <= 5;
      const isWorkHour = h >= 9 && h <= 18;
      const base = isWorkDay && isWorkHour ? 5 : 0;
      const count = Math.max(0, Math.round(base + Math.random() * 8 - 2));
      if (count > 0) data.push([h, d, count]);
    }
  }
  return data;
}

const option = {
  title: { text: 'GitHub Commit Activity', left: 'center' },
  tooltip: {
    position: 'top',
    formatter: p => `${days[p.data[1]]} ${hours[p.data[0]]}: ${p.data[2]} commits`
  },
  grid: { height: '60%', top: '10%' },
  xAxis: {
    type: 'category',
    data: hours,
    splitArea: { show: true },
    axisLabel: { interval: 2 }
  },
  yAxis: {
    type: 'category',
    data: days,
    splitArea: { show: true }
  },
  visualMap: {
    min: 0,
    max: 12,
    calculable: true,
    orient: 'horizontal',
    left: 'center',
    bottom: '8%',
    inRange: { color: ['#ebedf0', '#9be9a8', '#40c463', '#30a14e', '#216e39'] }
  },
  series: [
    {
      name: 'Commits',
      type: 'heatmap',
      data: generateData(),
      label: { show: false },
      emphasis: {
        itemStyle: { shadowBlur: 10, shadowColor: 'rgba(0,0,0,0.5)' }
      }
    }
  ]
};
```

---

## Example 2 — Calendar Heatmap (GitHub Contributions Style)

**Use case**: Show daily activity over a full year in calendar format.  
**Editor**: [calendar-heatmap](https://echarts.apache.org/examples/en/editor.html?c=calendar-heatmap)

```js
// Generate a year of daily data
function generateYearData(year) {
  const data = [];
  const start = new Date(`${year}-01-01`);
  const end   = new Date(`${year}-12-31`);
  for (let d = new Date(start); d <= end; d.setDate(d.getDate() + 1)) {
    const dateStr = d.toISOString().slice(0, 10);
    // Higher values on weekdays
    const isWeekend = d.getDay() === 0 || d.getDay() === 6;
    const value = isWeekend
      ? Math.floor(Math.random() * 4)
      : Math.floor(Math.random() * 12);
    if (value > 0) data.push([dateStr, value]);
  }
  return data;
}

const year = 2024;

const option = {
  title: { top: 30, left: 'center', text: `${year} Code Contributions` },
  tooltip: {
    formatter: p => `${p.data[0]}: ${p.data[1]} contributions`
  },
  visualMap: {
    min: 0,
    max: 12,
    type: 'piecewise',
    orient: 'horizontal',
    left: 'center',
    bottom: 20,
    pieces: [
      { min: 0, max: 0, color: '#ebedf0', label: '0' },
      { min: 1, max: 3, color: '#9be9a8', label: '1-3' },
      { min: 4, max: 6, color: '#40c463', label: '4-6' },
      { min: 7, max: 9, color: '#30a14e', label: '7-9' },
      { min: 10,        color: '#216e39', label: '10+' }
    ],
    showLabel: true
  },
  calendar: {
    top: 80,
    left: 30,
    right: 30,
    cellSize: ['auto', 16],
    range: year,
    itemStyle: { borderWidth: 0.5 },
    yearLabel: { show: false }
  },
  series: [
    {
      type: 'heatmap',
      coordinateSystem: 'calendar',
      data: generateYearData(year)
    }
  ]
};
```

---

## Example 3 — Correlation Matrix Heatmap

**Use case**: Visualize pairwise correlation coefficients between variables.  
**Editor**: [heatmap-large-piecewise](https://echarts.apache.org/examples/en/editor.html?c=heatmap-large-piecewise)

```js
const variables = ['Temp', 'Humidity', 'Wind', 'Rain', 'UV Index', 'Pressure'];

// Symmetric correlation matrix (upper triangle = lower triangle)
const correlations = [
  [1.00,  0.75, -0.30, 0.50, 0.85, -0.60],
  [0.75,  1.00, -0.20, 0.65, 0.60, -0.55],
  [-0.30,-0.20,  1.00,-0.40,-0.25,  0.15],
  [0.50,  0.65, -0.40, 1.00, 0.30, -0.70],
  [0.85,  0.60, -0.25, 0.30, 1.00, -0.50],
  [-0.60,-0.55,  0.15,-0.70,-0.50,  1.00]
];

const data = [];
for (let i = 0; i < variables.length; i++) {
  for (let j = 0; j < variables.length; j++) {
    data.push([i, j, correlations[i][j]]);
  }
}

const option = {
  title: { text: 'Weather Variable Correlation Matrix', left: 'center' },
  tooltip: {
    formatter: p => `${variables[p.data[0]]} × ${variables[p.data[1]]}: ${p.data[2].toFixed(2)}`
  },
  grid: { top: '10%', bottom: '15%', left: '12%', right: '5%' },
  xAxis: {
    type: 'category',
    data: variables,
    splitArea: { show: true },
    axisLabel: { rotate: 30 }
  },
  yAxis: {
    type: 'category',
    data: variables,
    splitArea: { show: true }
  },
  visualMap: {
    min: -1,
    max: 1,
    calculable: true,
    orient: 'horizontal',
    left: 'center',
    bottom: '2%',
    inRange: {
      color: ['#4575b4', '#91bfdb', '#ffffbf', '#fdae61', '#d73027']
    }
  },
  series: [
    {
      type: 'heatmap',
      data: data,
      label: {
        show: true,
        formatter: p => p.data[2].toFixed(2),
        fontSize: 11
      },
      emphasis: {
        itemStyle: { shadowBlur: 10, shadowColor: 'rgba(0,0,0,0.5)' }
      }
    }
  ]
};
```
