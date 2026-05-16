# Chord Chart Examples (v6.0.0+)

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-chord  
> **Requires ECharts v6.0.0+**

---

## Example 1 — Basic Chord (Trade Flows)

**Use case**: Show bidirectional flows/volumes between categories.  
**Editor**: [chord-simple](https://echarts.apache.org/examples/en/editor.html?c=chord-simple)

```js
// ECharts v6+ only
const option = {
  title: { text: 'Global Trade Flows (Chord Diagram)', left: 'center' },
  tooltip: {
    formatter: params => params.dataType === 'node'
      ? `${params.name}: Total trade $${params.value}B`
      : `${params.data.source} → ${params.data.target}: $${params.data.value}B`
  },
  series: [
    {
      type: 'chord',
      radius: '65%',
      padAngle: 0.03,
      startAngle: 90,
      clockwise: true,
      itemStyle: {
        borderWidth: 1,
        borderColor: '#fff'
      },
      label: {
        show: true,
        fontSize: 13,
        formatter: '{b}: {c}B'
      },
      emphasis: { focus: 'adjacency' },
      data: [
        { name: 'China',  value: 520 },
        { name: 'USA',    value: 480 },
        { name: 'EU',     value: 440 },
        { name: 'Japan',  value: 180 },
        { name: 'India',  value: 150 },
        { name: 'Others', value: 230 }
      ],
      links: [
        { source: 'China',  target: 'USA',    value: 60 },
        { source: 'China',  target: 'EU',     value: 55 },
        { source: 'China',  target: 'Japan',  value: 35 },
        { source: 'China',  target: 'India',  value: 25 },
        { source: 'China',  target: 'Others', value: 40 },
        { source: 'USA',    target: 'EU',     value: 70 },
        { source: 'USA',    target: 'Japan',  value: 30 },
        { source: 'USA',    target: 'India',  value: 28 },
        { source: 'USA',    target: 'Others', value: 35 },
        { source: 'EU',     target: 'Japan',  value: 20 },
        { source: 'EU',     target: 'India',  value: 18 },
        { source: 'EU',     target: 'Others', value: 40 },
        { source: 'Japan',  target: 'India',  value: 10 },
        { source: 'India',  target: 'Others', value: 15 }
      ]
    }
  ]
};
```

---

## Example 2 — Chord with Gradient Edges

**Use case**: Use color gradients on edges to show directionality.  
**Editor**: [chord-lineStyle-color](https://echarts.apache.org/examples/en/editor.html?c=chord-lineStyle-color)

```js
// ECharts v6+ only
const option = {
  title: { text: 'Team Communication Channels', left: 'center' },
  tooltip: {
    formatter: params => params.dataType === 'edge'
      ? `${params.data.source} → ${params.data.target}: ${params.data.value} messages/day`
      : `${params.name}`
  },
  series: [
    {
      type: 'chord',
      radius: '60%',
      padAngle: 0.05,
      lineStyle: {
        color: 'gradient',
        opacity: 0.6
      },
      label: { show: true, fontSize: 12 },
      emphasis: { focus: 'adjacency' },
      data: [
        { name: 'Engineering',  value: 100, itemStyle: { color: '#5470c6' } },
        { name: 'Product',      value: 80,  itemStyle: { color: '#91cc75' } },
        { name: 'Design',       value: 60,  itemStyle: { color: '#fac858' } },
        { name: 'Marketing',    value: 70,  itemStyle: { color: '#ee6666' } },
        { name: 'Sales',        value: 90,  itemStyle: { color: '#73c0de' } }
      ],
      links: [
        { source: 'Engineering', target: 'Product',   value: 45 },
        { source: 'Engineering', target: 'Design',    value: 30 },
        { source: 'Product',     target: 'Design',    value: 25 },
        { source: 'Product',     target: 'Marketing', value: 20 },
        { source: 'Product',     target: 'Sales',     value: 35 },
        { source: 'Design',      target: 'Marketing', value: 15 },
        { source: 'Marketing',   target: 'Sales',     value: 40 },
        { source: 'Engineering', target: 'Sales',     value: 18 }
      ]
    }
  ]
};
```

---

## Example 3 — Chord with minAngle

**Use case**: Prevent tiny slices from being invisible by setting a minimum arc angle.  
**Editor**: [chord-minAngle](https://echarts.apache.org/examples/en/editor.html?c=chord-minAngle)

```js
// ECharts v6+ only
const option = {
  title: { text: 'Programming Language Influence', left: 'center' },
  tooltip: { trigger: 'item' },
  series: [
    {
      type: 'chord',
      radius: '65%',
      padAngle: 0.02,
      minAngle: 5,       // prevent very small arcs
      itemStyle: { borderRadius: 4 },
      label: {
        show: true,
        formatter: '{b}',
        fontSize: 11
      },
      emphasis: {
        itemStyle: { shadowBlur: 10, shadowColor: 'rgba(0,0,0,0.3)' }
      },
      data: [
        { name: 'C',          value: 120 },
        { name: 'C++',        value: 100 },
        { name: 'Java',       value: 90 },
        { name: 'Python',     value: 110 },
        { name: 'JavaScript', value: 95 },
        { name: 'Go',         value: 40 },
        { name: 'Rust',       value: 30 },
        { name: 'Swift',      value: 25 },
        { name: 'Kotlin',     value: 20 }
      ],
      links: [
        { source: 'C',          target: 'C++',        value: 80 },
        { source: 'C',          target: 'Java',       value: 40 },
        { source: 'C',          target: 'Go',         value: 35 },
        { source: 'C',          target: 'Rust',       value: 30 },
        { source: 'C++',        target: 'Rust',       value: 25 },
        { source: 'Java',       target: 'Kotlin',     value: 60 },
        { source: 'Java',       target: 'Scala',      value: 30 },
        { source: 'JavaScript', target: 'TypeScript', value: 70 },
        { source: 'C',          target: 'Python',     value: 20 },
        { source: 'Java',       target: 'Python',     value: 15 },
        { source: 'C',          target: 'Swift',      value: 18 },
        { source: 'Java',       target: 'Swift',      value: 10 }
      ]
    }
  ]
};
```
