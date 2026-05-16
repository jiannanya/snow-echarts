# Funnel Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-funnel

---

## Example 1 — Sales Conversion Funnel

**Use case**: Show step-by-step drop-off in a conversion process.  
**Editor**: [funnel](https://echarts.apache.org/examples/en/editor.html?c=funnel)

```js
const option = {
  title: { text: 'Sales Conversion Funnel', left: 'center' },
  tooltip: {
    trigger: 'item',
    formatter: '{a}<br/>{b}: {c} ({d}%)'
  },
  legend: {
    data: ['Impressions', 'Clicks', 'Signups', 'Trials', 'Paid'],
    bottom: 10
  },
  series: [
    {
      name: 'Conversion',
      type: 'funnel',
      left: '15%',
      width: '70%',
      top: 60,
      bottom: 60,
      min: 0,
      max: 100,
      sort: 'descending',
      gap: 2,
      label: {
        show: true,
        position: 'inside',
        formatter: '{b}\n{c}k users',
        fontSize: 13,
        color: '#fff'
      },
      labelLine: { show: false },
      itemStyle: { borderColor: '#fff', borderWidth: 1 },
      emphasis: {
        label: { fontSize: 16, fontWeight: 'bold' }
      },
      data: [
        { value: 100, name: 'Impressions', itemStyle: { color: '#5470c6' } },
        { value: 40,  name: 'Clicks',      itemStyle: { color: '#91cc75' } },
        { value: 20,  name: 'Signups',     itemStyle: { color: '#fac858' } },
        { value: 10,  name: 'Trials',      itemStyle: { color: '#ee6666' } },
        { value: 4,   name: 'Paid',        itemStyle: { color: '#73c0de' } }
      ]
    }
  ]
};
```

---

## Example 2 — Comparison Funnel (Actual vs Target)

**Use case**: Side-by-side funnel comparing two scenarios.  
**Editor**: [funnel-align](https://echarts.apache.org/examples/en/editor.html?c=funnel-align)

```js
const option = {
  title: { text: 'Actual vs Target — Marketing Funnel', left: 'center' },
  tooltip: { trigger: 'item', formatter: '{a}<br/>{b}: {c}%' },
  legend: { data: ['Actual', 'Target'], bottom: 10 },
  series: [
    {
      name: 'Actual',
      type: 'funnel',
      left: '5%',
      width: '44%',
      min: 0, max: 100,
      sort: 'descending',
      gap: 2,
      label: { position: 'left', formatter: '{b}: {c}%' },
      data: [
        { value: 100, name: 'Awareness' },
        { value: 65,  name: 'Interest' },
        { value: 35,  name: 'Consideration' },
        { value: 20,  name: 'Intent' },
        { value: 10,  name: 'Purchase' }
      ]
    },
    {
      name: 'Target',
      type: 'funnel',
      left: '51%',
      width: '44%',
      min: 0, max: 100,
      sort: 'descending',
      gap: 2,
      label: { position: 'right', formatter: '{b}: {c}%' },
      data: [
        { value: 100, name: 'Awareness' },
        { value: 75,  name: 'Interest' },
        { value: 50,  name: 'Consideration' },
        { value: 30,  name: 'Intent' },
        { value: 18,  name: 'Purchase' }
      ]
    }
  ]
};
```

---

## Example 3 — Pyramid (Bottom-Up Funnel)

**Use case**: Display a data hierarchy or organizational pyramid.  
**Editor**: [funnel-customize](https://echarts.apache.org/examples/en/editor.html?c=funnel-customize)

```js
const option = {
  title: { text: 'Maslow\'s Hierarchy of Needs', left: 'center' },
  tooltip: { trigger: 'item', formatter: '{b}: {c}' },
  series: [
    {
      name: 'Hierarchy',
      type: 'funnel',
      sort: 'ascending',   // pyramid shape (small at bottom, large at top)
      left: '20%',
      width: '60%',
      top: 40,
      bottom: 40,
      min: 0, max: 100,
      gap: 4,
      label: {
        show: true,
        position: 'inside',
        color: '#fff',
        fontSize: 14,
        fontWeight: 'bold',
        formatter: '{b}'
      },
      itemStyle: {
        borderColor: '#fff',
        borderWidth: 2,
        borderRadius: 4
      },
      data: [
        { value: 20,  name: 'Self-\nActualization', itemStyle: { color: '#5470c6' } },
        { value: 35,  name: 'Esteem',               itemStyle: { color: '#91cc75' } },
        { value: 50,  name: 'Social',               itemStyle: { color: '#fac858' } },
        { value: 65,  name: 'Safety',               itemStyle: { color: '#ee6666' } },
        { value: 80,  name: 'Physiological',        itemStyle: { color: '#73c0de' } }
      ]
    }
  ]
};
```
