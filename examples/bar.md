# Bar Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-bar

---

## Example 1 — Grouped Bar with Labels

**Use case**: Compare multiple series side-by-side across categories.  
**Editor**: [bar-simple](https://echarts.apache.org/examples/en/editor.html?c=bar-simple)

```js
const option = {
  title: { text: 'Quarterly Revenue by Region', left: 'center' },
  tooltip: { trigger: 'axis', axisPointer: { type: 'shadow' } },
  legend: { top: 30, data: ['North', 'South', 'East', 'West'] },
  grid: { left: '3%', right: '4%', bottom: '3%', containLabel: true },
  xAxis: {
    type: 'category',
    data: ['Q1', 'Q2', 'Q3', 'Q4']
  },
  yAxis: { type: 'value', name: 'Revenue ($k)' },
  series: [
    {
      name: 'North',
      type: 'bar',
      data: [320, 332, 301, 334],
      label: { show: true, position: 'top', formatter: '${c}k' },
      itemStyle: { borderRadius: [4, 4, 0, 0] }
    },
    {
      name: 'South',
      type: 'bar',
      data: [220, 182, 191, 234],
      itemStyle: { borderRadius: [4, 4, 0, 0] }
    },
    {
      name: 'East',
      type: 'bar',
      data: [150, 232, 201, 154],
      itemStyle: { borderRadius: [4, 4, 0, 0] }
    },
    {
      name: 'West',
      type: 'bar',
      data: [98, 77, 101, 99],
      itemStyle: { borderRadius: [4, 4, 0, 0] }
    }
  ]
};
```

---

## Example 2 — Stacked Horizontal Bar (Population Pyramid)

**Use case**: Show composition and allow easy ranking comparison.  
**Editor**: [bar-y-category](https://echarts.apache.org/examples/en/editor.html?c=bar-y-category)

```js
const option = {
  title: { text: 'Department Headcount by Level', left: 'center' },
  tooltip: {
    trigger: 'axis',
    axisPointer: { type: 'shadow' },
    formatter: params => params.map(p => `${p.marker}${p.seriesName}: ${p.value}`).join('<br/>')
  },
  legend: { bottom: 10, data: ['Junior', 'Mid', 'Senior', 'Lead'] },
  grid: { left: '15%', right: '5%', bottom: '12%', containLabel: false },
  xAxis: { type: 'value', name: 'Headcount' },
  yAxis: {
    type: 'category',
    data: ['Engineering', 'Product', 'Design', 'Marketing', 'Sales'],
    axisLabel: { fontSize: 12 }
  },
  series: [
    { name: 'Junior',  type: 'bar', stack: 'total', data: [12, 5, 4, 8, 15] },
    { name: 'Mid',     type: 'bar', stack: 'total', data: [18, 8, 6, 10, 20] },
    { name: 'Senior',  type: 'bar', stack: 'total', data: [10, 4, 3, 4, 8] },
    { name: 'Lead',    type: 'bar', stack: 'total', data: [3, 2, 1, 2, 3],
      label: { show: true, position: 'right', formatter: p => `Total: ${
        [43, 19, 14, 24, 46][p.dataIndex]
      }` }
    }
  ]
};
```

---

## Example 3 — Bar Race (Dynamic Ranking)

**Use case**: Animate ranking changes over time.  
**Editor**: [bar-race](https://echarts.apache.org/examples/en/editor.html?c=bar-race)

```js
// Simulated year-by-year data
const years = [2018, 2019, 2020, 2021, 2022, 2023];
const rawData = {
  Chrome:  [63, 66, 67, 65, 66, 65],
  Safari:  [14, 15, 17, 19, 20, 20],
  Firefox: [13, 11, 9,  8,  8,  7],
  Edge:    [4,  5,  6,  9,  11, 12],
  Others:  [6,  3,  1,  -1, -5, -4]
};
let yearIdx = 0;

function buildOption(year) {
  const entries = Object.entries(rawData)
    .map(([name, vals]) => ({ name, value: vals[years.indexOf(year)] }))
    .sort((a, b) => a.value - b.value);
  return {
    graphic: [{ type: 'text', right: 60, bottom: 60,
      style: { text: year, font: 'bold 80px sans-serif', fill: 'rgba(100,100,100,0.25)' },
      z: 100 }],
    xAxis: { max: 'dataMax' },
    yAxis: { type: 'category', data: entries.map(e => e.name), animationDuration: 300, animationDurationUpdate: 1200 },
    series: [{
      realtimeSort: true, type: 'bar', seriesLayoutBy: 'row',
      data: entries.map(e => e.value),
      label: { show: true, position: 'right', valueAnimation: true }
    }],
    animationDuration: 0,
    animationDurationUpdate: 1200,
    animationEasing: 'linear',
    animationEasingUpdate: 'linear'
  };
}

const chart = echarts.init(document.getElementById('chart'));
chart.setOption({
  grid: { top: 10, bottom: 30, left: 150, right: 80 },
  xAxis: { max: 'dataMax', label: { show: true } },
  yAxis: { type: 'category', animationDuration: 300, animationDurationUpdate: 1200, max: 4 },
  series: [{ realtimeSort: true, type: 'bar', data: [], label: { show: true, position: 'right' } }],
  legend: { show: true },
  animationDurationUpdate: 1200,
  animationEasingUpdate: 'linear'
});

const timer = setInterval(() => {
  if (yearIdx >= years.length) { clearInterval(timer); return; }
  chart.setOption(buildOption(years[yearIdx++]));
}, 1500);
```
