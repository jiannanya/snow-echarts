# Treemap Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-treemap

---

## Example 1 — Basic Treemap (Disk Usage)

**Use case**: Show hierarchical space/size allocation with nested rectangles.  
**Editor**: [treemap-disk](https://echarts.apache.org/examples/en/editor.html?c=treemap-disk)

```js
const option = {
  title: { text: 'Codebase Size by Module', left: 'center' },
  tooltip: {
    formatter: info => {
      const value = info.value;
      return `<b>${info.name}</b><br/>Size: ${(value / 1024).toFixed(1)} KB`;
    }
  },
  series: [
    {
      name: 'Codebase',
      type: 'treemap',
      visibleMin: 300,
      roam: false,
      itemStyle: {
        borderColor: '#fff',
        borderWidth: 1,
        gapWidth: 1
      },
      upperLabel: {
        show: true,
        height: 30,
        color: '#fff',
        fontWeight: 'bold'
      },
      breadcrumb: { show: true },
      levels: [
        { itemStyle: { borderColor: '#555', borderWidth: 4, gapWidth: 4 }, upperLabel: { show: false } },
        { itemStyle: { borderColor: '#ddd', borderWidth: 2, gapWidth: 2 }, colorSaturation: [0.35, 0.5] },
        { colorSaturation: [0.35, 0.5], itemStyle: { borderColorSaturation: 0.6, gapWidth: 1, borderWidth: 1 } }
      ],
      data: [
        {
          name: 'frontend',
          children: [
            { name: 'components', value: 45000 },
            { name: 'pages',      value: 38000 },
            { name: 'styles',     value: 12000 },
            { name: 'hooks',      value: 8000 },
            { name: 'store',      value: 15000 }
          ]
        },
        {
          name: 'backend',
          children: [
            { name: 'api',        value: 52000 },
            { name: 'models',     value: 28000 },
            { name: 'services',   value: 35000 },
            { name: 'middleware', value: 10000 },
            { name: 'utils',      value: 6000 }
          ]
        },
        {
          name: 'shared',
          children: [
            { name: 'types',   value: 5000 },
            { name: 'helpers', value: 4000 },
            { name: 'config',  value: 2000 }
          ]
        },
        {
          name: 'tests',
          children: [
            { name: 'unit',        value: 30000 },
            { name: 'integration', value: 18000 },
            { name: 'e2e',         value: 12000 }
          ]
        }
      ]
    }
  ]
};
```

---

## Example 2 — Treemap with VisualMap (Color by Metric)

**Use case**: Color treemap rectangles by an additional metric (e.g., growth rate).  
**Editor**: [treemap-visual](https://echarts.apache.org/examples/en/editor.html?c=treemap-visual)

```js
const option = {
  title: { text: 'S&P 500 Sectors — Market Cap & Performance', left: 'center' },
  tooltip: {
    formatter: info => `
      <b>${info.name}</b><br/>
      Market Cap: $${(info.value / 1e12).toFixed(1)}T<br/>
      YTD Return: ${info.data.growth > 0 ? '+' : ''}${info.data.growth}%
    `
  },
  visualMap: {
    type: 'continuous',
    min: -15,
    max: 25,
    orient: 'horizontal',
    left: 'center',
    bottom: 20,
    inRange: { color: ['#d73027', '#fee090', '#4575b4'] },
    text: ['Positive Return', 'Negative Return']
  },
  series: [
    {
      type: 'treemap',
      data: [
        { name: 'Technology',     value: 12.5e12, growth: 18.5  },
        { name: 'Healthcare',     value: 5.8e12,  growth: 8.2   },
        { name: 'Financials',     value: 8.2e12,  growth: 12.1  },
        { name: 'Consumer Disc.', value: 4.5e12,  growth: -3.4  },
        { name: 'Industrials',    value: 3.8e12,  growth: 5.6   },
        { name: 'Communication',  value: 4.1e12,  growth: 14.3  },
        { name: 'Energy',         value: 2.9e12,  growth: -8.7  },
        { name: 'Utilities',      value: 1.5e12,  growth: -12.1 },
        { name: 'Materials',      value: 2.2e12,  growth: 2.3   },
        { name: 'Real Estate',    value: 1.8e12,  growth: -5.4  },
        { name: 'Staples',        value: 2.5e12,  growth: 1.2   }
      ].map(d => ({
        ...d,
        // Pass growth to visualMap via the `value` path or use colorValue
        label: { show: true, formatter: p => `${p.name}\n${p.data.growth > 0 ? '+' : ''}${p.data.growth}%` }
      })),
      visualDimension: 'growth',   // color by growth field
      itemStyle: { borderColor: '#fff', borderWidth: 1, gapWidth: 2 },
      breadcrumb: { show: false },
      label: { show: true, fontSize: 12 }
    }
  ]
};
```

---

## Example 3 — Drill-Down Treemap

**Use case**: Multi-level navigation — click a node to zoom into its children.  
**Editor**: [treemap-drill-down](https://echarts.apache.org/examples/en/editor.html?c=treemap-drill-down)

```js
const option = {
  title: { text: 'Global Revenue by Region → Country', left: 'center' },
  tooltip: { formatter: p => `${p.name}: $${(p.value / 1e9).toFixed(1)}B` },
  series: [
    {
      type: 'treemap',
      roam: false,
      nodeClick: 'zoomToNode',
      drillDownIcon: '▶',
      breadcrumb: { show: true, top: 'bottom', height: 32 },
      upperLabel: {
        show: true,
        height: 30,
        color: '#fff',
        fontWeight: 'bold',
        fontSize: 14
      },
      itemStyle: { borderColor: '#fff', borderWidth: 1, gapWidth: 2 },
      data: [
        {
          name: 'Americas',
          value: 85e9,
          children: [
            { name: 'USA',        value: 60e9 },
            { name: 'Canada',     value: 8e9 },
            { name: 'Brazil',     value: 10e9 },
            { name: 'Mexico',     value: 5e9 },
            { name: 'Argentina',  value: 2e9 }
          ]
        },
        {
          name: 'Europe',
          value: 62e9,
          children: [
            { name: 'Germany', value: 14e9 },
            { name: 'UK',      value: 12e9 },
            { name: 'France',  value: 10e9 },
            { name: 'Italy',   value: 8e9 },
            { name: 'Others',  value: 18e9 }
          ]
        },
        {
          name: 'Asia Pacific',
          value: 75e9,
          children: [
            { name: 'China',     value: 30e9 },
            { name: 'Japan',     value: 15e9 },
            { name: 'India',     value: 12e9 },
            { name: 'Korea',     value: 8e9 },
            { name: 'Southeast Asia', value: 10e9 }
          ]
        },
        {
          name: 'Rest of World',
          value: 18e9,
          children: [
            { name: 'Middle East', value: 8e9 },
            { name: 'Africa',      value: 5e9 },
            { name: 'Other',       value: 5e9 }
          ]
        }
      ]
    }
  ]
};
```
