# Pie Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-pie

---

## Example 1 — Doughnut with Center Label (KPI)

**Use case**: Show single KPI with a ring/donut highlighting part-to-whole.  
**Editor**: [pie-doughnut](https://echarts.apache.org/examples/en/editor.html?c=pie-doughnut)

```js
const option = {
  title: {
    text: 'Budget Allocation',
    subtext: 'FY 2024',
    left: 'center',
    top: 20
  },
  tooltip: { trigger: 'item', formatter: '{b}: {c} ({d}%)' },
  legend: { orient: 'vertical', left: 10, top: 'middle' },
  series: [
    {
      name: 'Budget',
      type: 'pie',
      radius: ['45%', '70%'],
      center: ['60%', '50%'],
      avoidLabelOverlap: false,
      padAngle: 3,
      itemStyle: { borderRadius: 8, borderColor: '#fff', borderWidth: 2 },
      label: {
        show: false,
        position: 'center'
      },
      emphasis: {
        label: {
          show: true,
          fontSize: 22,
          fontWeight: 'bold',
          formatter: '{b}\n{d}%'
        }
      },
      labelLine: { show: false },
      data: [
        { value: 1048, name: 'Engineering' },
        { value: 735,  name: 'Marketing' },
        { value: 580,  name: 'Operations' },
        { value: 484,  name: 'R&D' },
        { value: 300,  name: 'Admin' }
      ]
    }
  ]
};
```

---

## Example 2 — Nightingale Rose Chart

**Use case**: Show category comparison where both angle AND radius encode magnitude.  
**Editor**: [pie-roseType](https://echarts.apache.org/examples/en/editor.html?c=pie-roseType)

```js
const option = {
  title: { text: 'Monthly Downloads', left: 'center' },
  tooltip: { trigger: 'item', formatter: '{b}: {c}k downloads ({d}%)' },
  legend: {
    orient: 'vertical',
    right: 10,
    top: 'middle',
    data: ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec']
  },
  series: [
    {
      name: 'Downloads',
      type: 'pie',
      radius: ['20%', '65%'],
      center: ['40%', '50%'],
      roseType: 'radius',          // radius encodes value magnitude
      itemStyle: { borderRadius: 5 },
      label: { show: true, formatter: '{b}\n{c}k' },
      emphasis: {
        itemStyle: { shadowBlur: 10, shadowColor: 'rgba(0,0,0,0.5)' }
      },
      data: [
        { value: 40,  name: 'Jan' }, { value: 38,  name: 'Feb' },
        { value: 32,  name: 'Mar' }, { value: 30,  name: 'Apr' },
        { value: 28,  name: 'May' }, { value: 26,  name: 'Jun' },
        { value: 22,  name: 'Jul' }, { value: 18,  name: 'Aug' },
        { value: 22,  name: 'Sep' }, { value: 28,  name: 'Oct' },
        { value: 36,  name: 'Nov' }, { value: 42,  name: 'Dec' }
      ]
    }
  ]
};
```

---

## Example 3 — Nested Pies (Multi-Level)

**Use case**: Represent a two-level hierarchy (outer = detail, inner = category).  
**Editor**: [pie-nest](https://echarts.apache.org/examples/en/editor.html?c=pie-nest)

```js
const option = {
  title: { text: 'Traffic Sources — Platform Breakdown', left: 'center' },
  tooltip: { trigger: 'item', formatter: '{a}<br/>{b}: {c} ({d}%)' },
  legend: { top: 30, data: ['Mobile', 'Desktop', 'Tablet', 'Organic', 'Paid', 'Direct', 'Social', 'Email', 'Other'] },
  series: [
    {
      name: 'Platform',
      type: 'pie',
      selectedMode: 'single',
      radius: [0, '35%'],
      label: { position: 'inner', fontSize: 13 },
      data: [
        { value: 1548, name: 'Mobile' },
        { value: 775,  name: 'Desktop' },
        { value: 274,  name: 'Tablet' }
      ]
    },
    {
      name: 'Source',
      type: 'pie',
      radius: ['42%', '65%'],
      labelLine: { length: 20 },
      label: {
        formatter: (params) => `${params.name}\n${params.percent}%`
      },
      data: [
        { value: 580, name: 'Organic' },
        { value: 484, name: 'Paid' },
        { value: 300, name: 'Direct' },
        { value: 184, name: 'Social' },
        { value: 735, name: 'Email' },
        { value: 315, name: 'Other' }
      ]
    }
  ]
};
```
