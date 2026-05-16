# Graph Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-graph

---

## Example 1 — Force-Layout Network Graph

**Use case**: Show relationships between entities (social networks, dependencies).  
**Editor**: [graph-force](https://echarts.apache.org/examples/en/editor.html?c=graph-force)

```js
const option = {
  title: { text: 'Technology Dependency Graph', left: 'center' },
  tooltip: { trigger: 'item' },
  legend: [{ data: ['Framework', 'Library', 'Tool', 'Runtime'] }],
  series: [
    {
      name: 'Dependencies',
      type: 'graph',
      layout: 'force',
      roam: true,
      draggable: true,
      force: {
        repulsion: 400,
        edgeLength: [80, 150],
        gravity: 0.1
      },
      label: { show: true, position: 'right', fontSize: 11 },
      lineStyle: { color: '#aaa', opacity: 0.7, curveness: 0.1 },
      emphasis: {
        focus: 'adjacency',
        lineStyle: { width: 4 }
      },
      categories: [
        { name: 'Framework', itemStyle: { color: '#5470c6' } },
        { name: 'Library',   itemStyle: { color: '#91cc75' } },
        { name: 'Tool',      itemStyle: { color: '#fac858' } },
        { name: 'Runtime',   itemStyle: { color: '#ee6666' } }
      ],
      data: [
        { id: '0',  name: 'React',      symbolSize: 50, category: 0 },
        { id: '1',  name: 'Vue',        symbolSize: 45, category: 0 },
        { id: '2',  name: 'Node.js',    symbolSize: 48, category: 3 },
        { id: '3',  name: 'TypeScript', symbolSize: 42, category: 2 },
        { id: '4',  name: 'Vite',       symbolSize: 35, category: 2 },
        { id: '5',  name: 'Redux',      symbolSize: 30, category: 1 },
        { id: '6',  name: 'Axios',      symbolSize: 28, category: 1 },
        { id: '7',  name: 'Jest',       symbolSize: 30, category: 2 },
        { id: '8',  name: 'ESLint',     symbolSize: 28, category: 2 },
        { id: '9',  name: 'Express',    symbolSize: 38, category: 0 },
        { id: '10', name: 'Webpack',    symbolSize: 32, category: 2 },
        { id: '11', name: 'Lodash',     symbolSize: 25, category: 1 }
      ],
      links: [
        { source: '0', target: '3' }, { source: '0', target: '5' },
        { source: '0', target: '4' }, { source: '0', target: '7' },
        { source: '1', target: '3' }, { source: '1', target: '4' },
        { source: '2', target: '9' }, { source: '2', target: '3' },
        { source: '2', target: '6' }, { source: '4', target: '10' },
        { source: '9', target: '6' }, { source: '7', target: '8' },
        { source: '0', target: '6' }, { source: '9', target: '11' },
        { source: '2', target: '11' }
      ]
    }
  ]
};
```

---

## Example 2 — Circular Graph (Chord-Like)

**Use case**: Compact circular layout for dense networks where layout order matters.  
**Editor**: [graph-circular-layout](https://echarts.apache.org/examples/en/editor.html?c=graph-circular-layout)

```js
const teamMembers = ['Alice', 'Bob', 'Carol', 'Dave', 'Eve', 'Frank', 'Grace', 'Hank'];
const collaborations = [
  ['Alice', 'Bob', 12],   ['Alice', 'Carol', 8],   ['Alice', 'Dave', 5],
  ['Bob',   'Carol', 15], ['Bob',   'Frank', 7],   ['Carol', 'Eve', 10],
  ['Dave',  'Eve', 6],    ['Dave',  'Grace', 9],   ['Eve',   'Frank', 4],
  ['Frank', 'Grace', 11], ['Grace', 'Hank', 8],    ['Hank',  'Alice', 6]
];

const option = {
  title: { text: 'Team Collaboration Network', left: 'center' },
  tooltip: {
    formatter: params => params.dataType === 'edge'
      ? `${params.data.source} ↔ ${params.data.target}: ${params.data.value} sessions`
      : params.name
  },
  series: [
    {
      type: 'graph',
      layout: 'circular',
      circular: { rotateLabel: true },
      roam: true,
      label: { show: true, position: 'outside', fontSize: 12, color: '#333' },
      edgeSymbol: ['none', 'none'],
      lineStyle: {
        color: '#aaa',
        opacity: 0.6,
        curveness: 0.3,
        width: p => Math.max(1, p.data.value / 5)
      },
      emphasis: {
        focus: 'adjacency',
        lineStyle: { width: 4, color: '#5470c6' }
      },
      data: teamMembers.map(name => ({
        name,
        symbolSize: 40,
        itemStyle: {
          color: ['#5470c6', '#91cc75', '#fac858', '#ee6666', '#73c0de', '#3ba272', '#fc8452', '#9a60b4'][
            teamMembers.indexOf(name)
          ]
        }
      })),
      links: collaborations.map(([source, target, value]) => ({ source, target, value }))
    }
  ]
};
```

---

## Example 3 — Graph on Cartesian (Timeline-Based)

**Use case**: Position nodes on an actual axis system when coordinates are meaningful.  
**Editor**: [graph-grid](https://echarts.apache.org/examples/en/editor.html?c=graph-grid)

```js
// Project dependency timeline
const tasks = [
  { name: 'Requirements', x: 1,  y: 3, duration: 2 },
  { name: 'Design',       x: 3,  y: 4, duration: 3 },
  { name: 'Architecture', x: 3,  y: 2, duration: 2 },
  { name: 'Frontend',     x: 6,  y: 4, duration: 5 },
  { name: 'Backend',      x: 5,  y: 2, duration: 5 },
  { name: 'Integration',  x: 10, y: 3, duration: 2 },
  { name: 'Testing',      x: 12, y: 3, duration: 2 },
  { name: 'Deployment',   x: 14, y: 3, duration: 1 }
];

const deps = [
  [0, 1], [0, 2], [1, 3], [2, 4], [3, 5], [4, 5], [5, 6], [6, 7]
];

const option = {
  title: { text: 'Project Dependency Timeline', left: 'center' },
  tooltip: { formatter: p => p.dataType === 'node' ? `${p.name} (Week ${p.data.x})` : '' },
  grid: { left: '5%', right: '5%', top: '10%', bottom: '15%' },
  xAxis: { min: 0, max: 16, name: 'Week', nameLocation: 'middle', nameGap: 25 },
  yAxis: { min: 0, max: 6, name: 'Priority Lane', show: false },
  series: [
    {
      type: 'graph',
      coordinateSystem: 'cartesian2d',
      edgeSymbol: ['none', 'arrow'],
      edgeSymbolSize: 10,
      label: { show: true, position: 'inside', fontSize: 9, color: '#fff' },
      lineStyle: { color: '#aaa', curveness: 0.2 },
      itemStyle: { color: '#5470c6' },
      symbolSize: [80, 36],
      symbol: 'rect',
      data: tasks.map(t => ({
        name: t.name,
        x: t.x,
        y: t.y,
        value: [t.x, t.y]
      })),
      links: deps.map(([s, e]) => ({
        source: tasks[s].name,
        target: tasks[e].name
      }))
    }
  ]
};
```
