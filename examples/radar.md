# Radar Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-radar

---

## Example 1 — Multi-Series Radar (Team Comparison)

**Use case**: Compare multiple entities across the same set of attributes.  
**Editor**: [radar](https://echarts.apache.org/examples/en/editor.html?c=radar)

```js
const option = {
  title: { text: 'Product Feature Comparison', left: 'center' },
  tooltip: { trigger: 'item' },
  legend: { bottom: 10, data: ['Product A', 'Product B', 'Product C'] },
  radar: {
    indicator: [
      { name: 'Performance',  max: 100 },
      { name: 'Reliability',  max: 100 },
      { name: 'Ease of Use',  max: 100 },
      { name: 'Features',     max: 100 },
      { name: 'Support',      max: 100 },
      { name: 'Price/Value',  max: 100 }
    ],
    shape: 'circle',
    splitNumber: 4,
    axisName: { color: '#333', fontSize: 13 },
    splitLine: { lineStyle: { color: ['#ddd'] } }
  },
  series: [
    {
      name: 'Comparison',
      type: 'radar',
      data: [
        {
          value: [85, 90, 78, 88, 80, 75],
          name: 'Product A',
          areaStyle: { opacity: 0.2 },
          lineStyle: { width: 2 }
        },
        {
          value: [70, 75, 92, 80, 70, 88],
          name: 'Product B',
          areaStyle: { opacity: 0.2 },
          lineStyle: { width: 2 }
        },
        {
          value: [88, 80, 72, 95, 65, 72],
          name: 'Product C',
          areaStyle: { opacity: 0.2 },
          lineStyle: { width: 2 }
        }
      ]
    }
  ]
};
```

---

## Example 2 — AQI Radar (filled, custom colors)

**Use case**: Show environmental quality across pollutants for different cities.  
**Editor**: [radar-aqi](https://echarts.apache.org/examples/en/editor.html?c=radar-aqi)

```js
const option = {
  title: { text: 'Air Quality Index by City', left: 'center' },
  tooltip: {
    trigger: 'item',
    formatter: params => {
      const indicators = ['PM2.5', 'PM10', 'CO', 'NO₂', 'SO₂', 'O₃'];
      return params.data.value
        .map((v, i) => `${indicators[i]}: ${v}`)
        .join('<br/>');
    }
  },
  legend: { bottom: 10, data: ['Beijing', 'Los Angeles', 'London'] },
  radar: {
    indicator: [
      { name: 'PM2.5', max: 200 },
      { name: 'PM10',  max: 300 },
      { name: 'CO',    max: 5 },
      { name: 'NO₂',  max: 150 },
      { name: 'SO₂',  max: 100 },
      { name: 'O₃',   max: 200 }
    ],
    splitArea: {
      areaStyle: {
        color: ['rgba(255,255,255,0.2)', 'rgba(255,255,255,0.1)',
                'rgba(200,200,200,0.1)', 'rgba(200,200,200,0.2)'],
        shadowBlur: 5
      }
    }
  },
  series: [
    {
      type: 'radar',
      data: [
        {
          value: [80, 120, 1.8, 80, 40, 100],
          name: 'Beijing',
          symbol: 'circle',
          symbolSize: 6,
          lineStyle: { color: '#ee6666' },
          areaStyle: { color: 'rgba(238,102,102,0.3)' }
        },
        {
          value: [30, 60, 0.6, 50, 10, 120],
          name: 'Los Angeles',
          symbol: 'rect',
          symbolSize: 6,
          lineStyle: { color: '#5470c6' },
          areaStyle: { color: 'rgba(84,112,198,0.3)' }
        },
        {
          value: [20, 45, 0.4, 35, 15, 90],
          name: 'London',
          symbol: 'diamond',
          symbolSize: 6,
          lineStyle: { color: '#91cc75' },
          areaStyle: { color: 'rgba(145,204,117,0.3)' }
        }
      ]
    }
  ]
};
```

---

## Example 3 — Skills Assessment Radar

**Use case**: Visualize an individual's competency scores across multiple skills.  
**Editor**: [radar-custom](https://echarts.apache.org/examples/en/editor.html?c=radar-custom)

```js
const option = {
  title: { text: 'Developer Skills Assessment', left: 'center' },
  tooltip: { trigger: 'item' },
  legend: { bottom: 10, data: ['Alice', 'Bob', 'Target'] },
  radar: {
    indicator: [
      { name: 'Frontend',   max: 10 },
      { name: 'Backend',    max: 10 },
      { name: 'DevOps',     max: 10 },
      { name: 'Testing',    max: 10 },
      { name: 'Database',   max: 10 },
      { name: 'Security',   max: 10 },
      { name: 'AI/ML',      max: 10 }
    ],
    radius: '65%',
    startAngle: 90,
    shape: 'polygon'
  },
  series: [
    {
      type: 'radar',
      data: [
        {
          value: [9, 7, 5, 8, 6, 7, 4],
          name: 'Alice',
          areaStyle: { opacity: 0.15 },
          lineStyle: { width: 2 },
          label: { show: true, formatter: p => p.value }
        },
        {
          value: [6, 9, 8, 6, 9, 5, 7],
          name: 'Bob',
          areaStyle: { opacity: 0.15 },
          lineStyle: { width: 2 },
          label: { show: true, formatter: p => p.value }
        },
        {
          value: [8, 8, 7, 8, 8, 8, 7],
          name: 'Target',
          lineStyle: { type: 'dashed', color: '#aaa', width: 1 },
          areaStyle: { opacity: 0.05 },
          itemStyle: { color: 'transparent' }
        }
      ]
    }
  ]
};
```
