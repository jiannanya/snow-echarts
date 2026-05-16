# Sankey Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-sankey

---

## Example 1 — Energy Flow Sankey

**Use case**: Show how a quantity (energy, money, traffic) flows through a system.  
**Editor**: [sankey-simple](https://echarts.apache.org/examples/en/editor.html?c=sankey-simple)

```js
const option = {
  title: { text: 'Energy Flow Diagram', left: 'center' },
  tooltip: {
    trigger: 'item',
    triggerOn: 'mousemove',
    formatter: params => params.dataType === 'node'
      ? `${params.name}`
      : `${params.data.source} → ${params.data.target}: ${params.data.value} TWh`
  },
  series: [
    {
      type: 'sankey',
      layout: 'none',
      emphasis: { focus: 'adjacency' },
      nodeWidth: 20,
      nodePadding: 10,
      lineStyle: { color: 'gradient', opacity: 0.4, curveness: 0.5 },
      label: { color: '#000', fontSize: 12 },
      data: [
        { name: 'Coal'         },
        { name: 'Natural Gas'  },
        { name: 'Renewables'   },
        { name: 'Nuclear'      },
        { name: 'Electricity'  },
        { name: 'Heat'         },
        { name: 'Industry'     },
        { name: 'Transport'    },
        { name: 'Residential'  },
        { name: 'Losses'       }
      ],
      links: [
        { source: 'Coal',        target: 'Electricity', value: 150 },
        { source: 'Coal',        target: 'Heat',        value: 50 },
        { source: 'Natural Gas', target: 'Electricity', value: 80 },
        { source: 'Natural Gas', target: 'Heat',        value: 60 },
        { source: 'Natural Gas', target: 'Industry',    value: 40 },
        { source: 'Renewables',  target: 'Electricity', value: 120 },
        { source: 'Nuclear',     target: 'Electricity', value: 70 },
        { source: 'Electricity', target: 'Industry',    value: 180 },
        { source: 'Electricity', target: 'Transport',   value: 60 },
        { source: 'Electricity', target: 'Residential', value: 120 },
        { source: 'Electricity', target: 'Losses',      value: 60 },
        { source: 'Heat',        target: 'Industry',    value: 50 },
        { source: 'Heat',        target: 'Residential', value: 40 },
        { source: 'Heat',        target: 'Losses',      value: 20 }
      ]
    }
  ]
};
```

---

## Example 2 — Customer Journey Sankey

**Use case**: Visualize user flow and conversion funnels across stages.  
**Editor**: [sankey-vertical](https://echarts.apache.org/examples/en/editor.html?c=sankey-vertical)

```js
const option = {
  title: { text: 'Customer Journey — Website Funnel', left: 'center' },
  tooltip: {
    trigger: 'item',
    formatter: p => p.dataType === 'edge'
      ? `${p.data.source} → ${p.data.target}: ${p.data.value.toLocaleString()} users`
      : `${p.name}`
  },
  series: [
    {
      type: 'sankey',
      orient: 'vertical',    // top-to-bottom flow
      nodeAlign: 'justify',
      emphasis: { focus: 'adjacency' },
      nodeWidth: 20,
      nodePadding: 20,
      lineStyle: { color: 'source', opacity: 0.3, curveness: 0.5 },
      label: { fontSize: 11 },
      data: [
        // Stage 0: Acquisition
        { name: 'Organic Search', depth: 0, itemStyle: { color: '#5470c6' } },
        { name: 'Paid Ads',       depth: 0, itemStyle: { color: '#91cc75' } },
        { name: 'Social',         depth: 0, itemStyle: { color: '#fac858' } },
        { name: 'Direct',         depth: 0, itemStyle: { color: '#ee6666' } },
        // Stage 1: Landing
        { name: 'Home Page',     depth: 1 },
        { name: 'Product Page',  depth: 1 },
        // Stage 2: Engagement
        { name: 'Add to Cart',   depth: 2 },
        { name: 'Bounce',        depth: 2, itemStyle: { color: '#bbb' } },
        // Stage 3: Conversion
        { name: 'Checkout',      depth: 3 },
        { name: 'Abandoned',     depth: 3, itemStyle: { color: '#bbb' } },
        // Stage 4: Outcome
        { name: 'Purchase',      depth: 4, itemStyle: { color: '#3ba272' } },
        { name: 'Lost',          depth: 4, itemStyle: { color: '#bbb' } }
      ],
      links: [
        { source: 'Organic Search', target: 'Home Page',    value: 5000 },
        { source: 'Organic Search', target: 'Product Page', value: 3000 },
        { source: 'Paid Ads',       target: 'Product Page', value: 4000 },
        { source: 'Paid Ads',       target: 'Home Page',    value: 1000 },
        { source: 'Social',         target: 'Home Page',    value: 2000 },
        { source: 'Direct',         target: 'Home Page',    value: 1500 },
        { source: 'Home Page',      target: 'Add to Cart',  value: 3200 },
        { source: 'Home Page',      target: 'Bounce',       value: 6300 },
        { source: 'Product Page',   target: 'Add to Cart',  value: 5000 },
        { source: 'Product Page',   target: 'Bounce',       value: 2000 },
        { source: 'Add to Cart',    target: 'Checkout',     value: 6000 },
        { source: 'Add to Cart',    target: 'Abandoned',    value: 2200 },
        { source: 'Checkout',       target: 'Purchase',     value: 4800 },
        { source: 'Checkout',       target: 'Lost',         value: 1200 }
      ]
    }
  ]
};
```

---

## Example 3 — Sankey with Custom Node Styles

**Use case**: Distinguish node types visually with per-node colors and levels.  
**Editor**: [sankey-levels](https://echarts.apache.org/examples/en/editor.html?c=sankey-levels)

```js
const option = {
  title: { text: 'Budget Allocation Flow', left: 'center' },
  tooltip: {
    trigger: 'item',
    formatter: p => p.dataType === 'edge'
      ? `${p.data.source} → ${p.data.target}: $${(p.data.value / 1e6).toFixed(1)}M`
      : `${p.name}`
  },
  series: [
    {
      type: 'sankey',
      emphasis: { focus: 'adjacency' },
      levels: [
        { depth: 0, itemStyle: { color: '#1f77b4' }, lineStyle: { color: 'source', opacity: 0.2 } },
        { depth: 1, itemStyle: { color: '#2ca02c' }, lineStyle: { color: 'source', opacity: 0.3 } },
        { depth: 2, itemStyle: { color: '#ff7f0e' }, lineStyle: { color: 'source', opacity: 0.4 } }
      ],
      nodeWidth: 18,
      nodePadding: 12,
      label: { fontSize: 11 },
      data: [
        { name: 'Total Budget' },
        { name: 'Product R&D' },
        { name: 'Sales & Marketing' },
        { name: 'G&A' },
        { name: 'Frontend Dev' },
        { name: 'Backend Dev' },
        { name: 'AI Research' },
        { name: 'Digital Marketing' },
        { name: 'Field Sales' },
        { name: 'HR' },
        { name: 'Finance' }
      ],
      links: [
        { source: 'Total Budget', target: 'Product R&D',         value: 45e6 },
        { source: 'Total Budget', target: 'Sales & Marketing',   value: 35e6 },
        { source: 'Total Budget', target: 'G&A',                 value: 20e6 },
        { source: 'Product R&D',  target: 'Frontend Dev',        value: 15e6 },
        { source: 'Product R&D',  target: 'Backend Dev',         value: 18e6 },
        { source: 'Product R&D',  target: 'AI Research',         value: 12e6 },
        { source: 'Sales & Marketing', target: 'Digital Marketing', value: 20e6 },
        { source: 'Sales & Marketing', target: 'Field Sales',    value: 15e6 },
        { source: 'G&A',          target: 'HR',                  value: 10e6 },
        { source: 'G&A',          target: 'Finance',             value: 10e6 }
      ]
    }
  ]
};
```
