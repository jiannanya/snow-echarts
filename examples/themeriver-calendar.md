# ThemeRiver & Calendar Chart Examples

> Official examples:  
> - ThemeRiver: https://echarts.apache.org/examples/en/index.html#chart-type-themeRiver  
> - Calendar: https://echarts.apache.org/examples/en/index.html#chart-type-calendar

---

## ThemeRiver — Example 1: Basic Topic Stream

**Use case**: Show how multiple topic volumes evolve over time with flowing, organic shapes.  
**Editor**: [themeRiver-basic](https://echarts.apache.org/examples/en/editor.html?c=themeRiver-basic)

```js
// Data: [timestamp, value, topic]
const generateStream = () => {
  const topics = ['JavaScript', 'Python', 'Java', 'TypeScript', 'Go', 'Rust'];
  const data = [];
  for (let month = 1; month <= 24; month++) {
    const date = new Date(2022, month - 1, 1).toISOString().slice(0, 10);
    topics.forEach((topic, i) => {
      // Each topic has a different trend
      const trend = [1.2, 0.9, 1.0, 1.3, 0.8, 0.7][i];
      const base  = [80,  70,  60,  50,  30,  20][i];
      const value = Math.max(5, Math.round(base * trend + Math.random() * 20 - 10));
      data.push([date, value, topic]);
    });
  }
  return data;
};

const option = {
  title: { text: 'Programming Language Popularity Trends', left: 'center' },
  tooltip: {
    trigger: 'axis',
    axisPointer: { type: 'line' }
  },
  legend: {
    data: ['JavaScript', 'Python', 'Java', 'TypeScript', 'Go', 'Rust'],
    bottom: 10
  },
  singleAxis: {
    top: 60,
    bottom: 50,
    type: 'time',
    axisPointer: {
      animation: true,
      label: { show: true }
    }
  },
  series: [
    {
      type: 'themeRiver',
      emphasis: {
        itemStyle: { shadowBlur: 20, shadowColor: 'rgba(0,0,0,0.8)' }
      },
      data: generateStream()
    }
  ]
};
```

---

## ThemeRiver — Example 2: Music Genre Trends

**Use case**: Visualize how listener volumes for different genres shifted over years.  
**Editor**: [themeRiver-lastfm](https://echarts.apache.org/examples/en/editor.html?c=themeRiver-lastfm)

```js
const genres = ['Pop', 'Rock', 'Hip-Hop', 'Electronic', 'Country', 'Jazz'];
const years  = ['2015', '2016', '2017', '2018', '2019', '2020', '2021', '2022', '2023'];
const trends = [
  [85, 88, 90, 92, 95, 98, 100, 102, 105], // Pop
  [70, 68, 65, 62, 60, 58, 55, 53, 50],    // Rock declining
  [50, 60, 70, 78, 85, 90, 95, 100, 110],  // Hip-Hop rising
  [40, 45, 52, 60, 65, 70, 75, 80, 88],    // Electronic
  [30, 31, 32, 33, 34, 35, 36, 37, 38],    // Country steady
  [20, 19, 18, 17, 16, 15, 14, 13, 12]     // Jazz declining
];

const data = [];
years.forEach((year, yi) => {
  genres.forEach((genre, gi) => {
    data.push([year, trends[gi][yi], genre]);
  });
});

const option = {
  title: { text: 'Music Genre Popularity 2015–2023', left: 'center' },
  tooltip: { trigger: 'axis', axisPointer: { type: 'line' } },
  legend: { data: genres, bottom: 10 },
  singleAxis: {
    top: 60, bottom: 50,
    type: 'category',
    data: years,
    axisPointer: { animation: true, label: { show: true } }
  },
  series: [
    {
      type: 'themeRiver',
      emphasis: { itemStyle: { shadowBlur: 20 } },
      data: data
    }
  ]
};
```

---

## Calendar — Example 1: GitHub Contribution Heatmap

**Use case**: Show daily activity intensity across a full calendar year.  
**Editor**: [calendar-heatmap](https://echarts.apache.org/examples/en/editor.html?c=calendar-heatmap)

```js
function generateCalendarData(year) {
  const data = [];
  const start = new Date(`${year}-01-01`);
  const end   = new Date(`${year}-12-31`);
  for (let d = new Date(start); d <= end; d.setDate(d.getDate() + 1)) {
    const isWeekend = d.getDay() === 0 || d.getDay() === 6;
    const value = isWeekend
      ? Math.floor(Math.random() * 3)
      : Math.floor(Math.random() * 10 + 1);
    data.push([d.toISOString().slice(0, 10), value]);
  }
  return data;
}

const year = 2024;
const option = {
  title: { top: 30, left: 'center', text: `${year} Contribution Activity` },
  tooltip: { formatter: p => `${p.data[0]}: ${p.data[1]} contributions` },
  visualMap: {
    min: 0, max: 12,
    type: 'piecewise',
    orient: 'horizontal',
    left: 'center',
    bottom: 20,
    pieces: [
      { value: 0, color: '#ebedf0' },
      { min: 1, max: 3,  color: '#9be9a8' },
      { min: 4, max: 6,  color: '#40c463' },
      { min: 7, max: 9,  color: '#30a14e' },
      { min: 10,         color: '#216e39' }
    ]
  },
  calendar: {
    top: 80,
    left: 30,
    right: 30,
    cellSize: ['auto', 14],
    range: year,
    itemStyle: { borderWidth: 0.5, borderColor: '#fff' },
    yearLabel: { show: false }
  },
  series: [
    {
      type: 'heatmap',
      coordinateSystem: 'calendar',
      data: generateCalendarData(year)
    }
  ]
};
```

---

## Calendar — Example 2: Calendar + Scatter (Event Marking)

**Use case**: Overlay event markers on calendar cells to highlight notable dates.  
**Editor**: [calendar-effectscatter](https://echarts.apache.org/examples/en/editor.html?c=calendar-effectscatter)

```js
const year = 2024;

// Generate background heatmap data
const heatData = [];
for (let m = 0; m < 12; m++) {
  const daysInMonth = new Date(year, m + 1, 0).getDate();
  for (let d = 1; d <= daysInMonth; d++) {
    const date = `${year}-${String(m + 1).padStart(2, '0')}-${String(d).padStart(2, '0')}`;
    heatData.push([date, Math.round(Math.random() * 8)]);
  }
}

// Special events
const events = [
  { date: `${year}-01-15`, name: 'Product Launch' },
  { date: `${year}-03-20`, name: 'Spring Update' },
  { date: `${year}-06-10`, name: 'Summer Conference' },
  { date: `${year}-09-05`, name: 'Q3 Release' },
  { date: `${year}-11-25`, name: 'Black Friday' }
];

const option = {
  title: { top: 30, left: 'center', text: `${year} Events & Activity` },
  tooltip: { formatter: p => p.data.length === 2 ? `${p.data[0]}: ${p.data[1]} events` : p.data[0] },
  legend: { bottom: 20, data: ['Activity', 'Key Events'] },
  visualMap: {
    min: 0, max: 8,
    orient: 'horizontal',
    left: 'center',
    bottom: 45,
    inRange: { color: ['#e0f3f8', '#2166ac'] }
  },
  calendar: {
    top: 80, left: 30, right: 30,
    cellSize: ['auto', 14],
    range: year,
    itemStyle: { borderWidth: 0.5 }
  },
  series: [
    {
      name: 'Activity',
      type: 'heatmap',
      coordinateSystem: 'calendar',
      data: heatData
    },
    {
      name: 'Key Events',
      type: 'effectScatter',
      coordinateSystem: 'calendar',
      symbolSize: 10,
      rippleEffect: { brushType: 'fill', scale: 2 },
      itemStyle: { color: '#ee6666' },
      label: {
        show: true,
        position: 'top',
        formatter: p => events.find(e => e.date === p.data[0])?.name || '',
        fontSize: 9,
        color: '#333'
      },
      data: events.map(e => [e.date, 1])
    }
  ]
};
```
