# Sunburst Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-sunburst

---

## Example 1 — Basic Sunburst with Drill-Down

**Use case**: Multi-level hierarchy with click-to-zoom navigation.  
**Editor**: [sunburst-simple](https://echarts.apache.org/examples/en/editor.html?c=sunburst-simple)

```js
const option = {
  title: { text: 'Company Budget Breakdown', left: 'center' },
  tooltip: { formatter: p => `${p.name}: $${(p.value / 1e6).toFixed(1)}M` },
  series: [
    {
      type: 'sunburst',
      radius: ['10%', '90%'],
      nodeClick: 'rootToNode',
      emphasis: { focus: 'ancestor' },
      itemStyle: { borderRadius: 4, borderWidth: 1, borderColor: '#fff' },
      label: { fontSize: 11 },
      data: [
        {
          name: 'Engineering',
          value: 50,
          itemStyle: { color: '#5470c6' },
          children: [
            { name: 'Frontend',  value: 12, children: [{ name: 'Design Sys', value: 4 }, { name: 'Core App', value: 8 }] },
            { name: 'Backend',   value: 18, children: [{ name: 'API',     value: 10 }, { name: 'Data',     value: 8 }] },
            { name: 'DevOps',    value: 10, children: [{ name: 'Infra',   value: 6  }, { name: 'CI/CD',   value: 4 }] },
            { name: 'Mobile',    value: 10 }
          ]
        },
        {
          name: 'Marketing',
          value: 30,
          itemStyle: { color: '#91cc75' },
          children: [
            { name: 'Digital',  value: 15, children: [{ name: 'SEO', value: 5 }, { name: 'Ads', value: 10 }] },
            { name: 'Brand',    value: 8 },
            { name: 'Events',   value: 7 }
          ]
        },
        {
          name: 'Operations',
          value: 20,
          itemStyle: { color: '#fac858' },
          children: [
            { name: 'HR',       value: 8 },
            { name: 'Finance',  value: 7 },
            { name: 'Legal',    value: 5 }
          ]
        }
      ]
    }
  ]
};
```

---

## Example 2 — Sunburst with VisualMap Coloring

**Use case**: Color rings by value using a continuous color scale.  
**Editor**: [sunburst-visualMap](https://echarts.apache.org/examples/en/editor.html?c=sunburst-visualMap)

```js
// Flatten hierarchy to [depth, name, score] for color mapping
const option = {
  title: { text: 'Skill Coverage Map', left: 'center' },
  tooltip: { formatter: p => `${p.name}: ${p.value} proficiency` },
  visualMap: {
    min: 0,
    max: 100,
    orient: 'vertical',
    right: 10,
    top: 'middle',
    inRange: { color: ['#ef5350', '#ffa726', '#66bb6a'] },
    text: ['Expert', 'Beginner']
  },
  series: [
    {
      type: 'sunburst',
      radius: ['15%', '85%'],
      emphasis: { focus: 'self' },
      levels: [
        {},
        { r0: '15%', r: '40%', label: { rotate: 'tangential', fontSize: 11 } },
        { r0: '40%', r: '70%', label: { fontSize: 10 } },
        { r0: '70%', r: '85%', label: { position: 'outside', padding: 3, silent: false }, itemStyle: { borderWidth: 3 } }
      ],
      data: [
        {
          name: 'Frontend',
          children: [
            { name: 'React',  value: 90, children: [{ name: 'Hooks', value: 88 }, { name: 'Context', value: 75 }] },
            { name: 'CSS',    value: 80, children: [{ name: 'Grid', value: 85 }, { name: 'Flexbox', value: 90 }] },
            { name: 'TS',     value: 75, children: [{ name: 'Types', value: 70 }, { name: 'Generics', value: 55 }] }
          ]
        },
        {
          name: 'Backend',
          children: [
            { name: 'Node',    value: 70, children: [{ name: 'Express', value: 75 }, { name: 'Fastify', value: 55 }] },
            { name: 'Python',  value: 65, children: [{ name: 'Django', value: 60 }, { name: 'FastAPI', value: 70 }] },
            { name: 'SQL',     value: 80, children: [{ name: 'Postgres', value: 82 }, { name: 'MySQL', value: 78 }] }
          ]
        },
        {
          name: 'DevOps',
          children: [
            { name: 'Docker', value: 75 },
            { name: 'K8s',    value: 50 },
            { name: 'CI/CD',  value: 70 }
          ]
        }
      ]
    }
  ]
};
```

---

## Example 3 — Monochrome Sunburst (Label Inside)

**Use case**: Clean, single-color sunburst for reports and presentations.  
**Editor**: [sunburst-monochrome](https://echarts.apache.org/examples/en/editor.html?c=sunburst-monochrome)

```js
const option = {
  title: { text: 'Content Library Breakdown', left: 'center' },
  tooltip: { formatter: p => `${p.name}: ${p.value} items` },
  backgroundColor: '#1a1a2e',
  series: [
    {
      type: 'sunburst',
      radius: ['10%', '90%'],
      center: ['50%', '50%'],
      sort: 'desc',
      emphasis: { focus: 'ancestor' },
      itemStyle: {
        color: 'none',
        borderColor: '#1a1a2e',
        borderWidth: 1
      },
      label: {
        color: '#ddd',
        fontSize: 11,
        rotate: 'radial'
      },
      data: [
        { name: 'Videos',  value: 240, itemStyle: { color: '#4169e1' }, children: [
          { name: 'Tutorials', value: 120, children: [{ name: 'Beginner', value: 60 }, { name: 'Advanced', value: 60 }] },
          { name: 'Webinars',  value: 80 },
          { name: 'Short Form', value: 40 }
        ]},
        { name: 'Articles', value: 580, itemStyle: { color: '#20b2aa' }, children: [
          { name: 'How-To',    value: 200 },
          { name: 'Deep Dive', value: 180 },
          { name: 'News',      value: 100 },
          { name: 'Case Study', value: 100 }
        ]},
        { name: 'Podcasts', value: 90, itemStyle: { color: '#9370db' }, children: [
          { name: 'Interviews', value: 50 },
          { name: 'Solo',       value: 40 }
        ]}
      ]
    }
  ]
};
```
