# Tree Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-tree

---

## Example 1 — Horizontal Collapsible Tree

**Use case**: Navigate large hierarchical structures (org charts, file trees) with collapse/expand.  
**Editor**: [tree-basic](https://echarts.apache.org/examples/en/editor.html?c=tree-basic)

```js
const option = {
  title: { text: 'Organization Chart', left: 'center' },
  tooltip: { trigger: 'item', triggerOn: 'mousemove' },
  series: [
    {
      type: 'tree',
      layout: 'orthogonal',
      orient: 'LR',           // left → right
      roam: true,
      expandAndCollapse: true,
      initialTreeDepth: 2,    // auto-collapse beyond depth 2
      symbolSize: 10,
      symbol: 'emptyCircle',
      label: {
        position: 'left',
        verticalAlign: 'middle',
        align: 'right',
        fontSize: 12
      },
      leaves: {
        label: {
          position: 'right',
          verticalAlign: 'middle',
          align: 'left'
        }
      },
      emphasis: { focus: 'descendant' },
      data: [
        {
          name: 'CEO',
          children: [
            {
              name: 'CTO',
              children: [
                { name: 'Frontend Lead', children: [{ name: 'Alice' }, { name: 'Bob' }] },
                { name: 'Backend Lead',  children: [{ name: 'Carol' }, { name: 'Dave' }, { name: 'Eve' }] },
                { name: 'DevOps Lead',   children: [{ name: 'Frank' }] }
              ]
            },
            {
              name: 'CMO',
              children: [
                { name: 'Brand',   children: [{ name: 'Grace' }, { name: 'Hank' }] },
                { name: 'Digital', children: [{ name: 'Iris' }] }
              ]
            },
            {
              name: 'CFO',
              children: [
                { name: 'Accounting', children: [{ name: 'Jack' }, { name: 'Kate' }] },
                { name: 'FP&A',       children: [{ name: 'Leo' }] }
              ]
            }
          ]
        }
      ],
      animationDuration: 550,
      animationDurationUpdate: 750
    }
  ]
};
```

---

## Example 2 — Radial Tree

**Use case**: Compact radial layout for deeply nested hierarchies.  
**Editor**: [tree-radial](https://echarts.apache.org/examples/en/editor.html?c=tree-radial)

```js
const option = {
  title: { text: 'File System Tree (Radial)', left: 'center' },
  tooltip: { trigger: 'item', triggerOn: 'mousemove' },
  series: [
    {
      type: 'tree',
      layout: 'radial',
      symbolSize: 7,
      roam: true,
      initialTreeDepth: 3,
      label: { fontSize: 9 },
      leaves: { label: { fontSize: 8 } },
      emphasis: { focus: 'descendant' },
      expandAndCollapse: true,
      animationDuration: 550,
      animationDurationUpdate: 750,
      data: [
        {
          name: 'root/',
          children: [
            {
              name: 'src/',
              children: [
                { name: 'components/', children: [{ name: 'Button.tsx' }, { name: 'Modal.tsx' }, { name: 'Table.tsx' }] },
                { name: 'pages/',      children: [{ name: 'Home.tsx' }, { name: 'About.tsx' }, { name: 'Dashboard.tsx' }] },
                { name: 'utils/',      children: [{ name: 'api.ts' }, { name: 'helpers.ts' }] },
                { name: 'store/',      children: [{ name: 'index.ts' }, { name: 'slices/' }] }
              ]
            },
            {
              name: 'public/',
              children: [{ name: 'icons/' }, { name: 'images/' }, { name: 'fonts/' }]
            },
            { name: 'package.json' },
            { name: 'tsconfig.json' },
            { name: '.gitignore' }
          ]
        }
      ]
    }
  ]
};
```

---

## Example 3 — Multiple Trees Side-by-Side

**Use case**: Compare two hierarchical structures in the same chart.  
**Editor**: [tree-legend](https://echarts.apache.org/examples/en/editor.html?c=tree-legend)

```js
const option = {
  title: { text: 'Before & After Refactor', left: 'center' },
  tooltip: { trigger: 'item', triggerOn: 'mousemove' },
  legend: { bottom: 0, data: ['Before', 'After'] },
  series: [
    {
      type: 'tree',
      name: 'Before',
      left: '3%', right: '52%',
      top: '8%', bottom: '8%',
      symbolSize: 7,
      label: { position: 'left', verticalAlign: 'middle', align: 'right', fontSize: 10 },
      leaves: { label: { position: 'right', verticalAlign: 'middle', align: 'left' } },
      emphasis: { focus: 'descendant' },
      expandAndCollapse: true,
      data: [
        {
          name: 'App',
          children: [
            { name: 'PageA', children: [{ name: 'ComponentX' }, { name: 'ComponentY' }, { name: 'ComponentZ' }] },
            { name: 'PageB', children: [{ name: 'ComponentX' }, { name: 'ComponentW' }] },
            { name: 'Utils', children: [{ name: 'Helper1' }, { name: 'Helper2' }, { name: 'Helper3' }] }
          ]
        }
      ]
    },
    {
      type: 'tree',
      name: 'After',
      left: '52%', right: '3%',
      top: '8%', bottom: '8%',
      symbolSize: 7,
      label: { position: 'left', verticalAlign: 'middle', align: 'right', fontSize: 10 },
      leaves: { label: { position: 'right', verticalAlign: 'middle', align: 'left' } },
      emphasis: { focus: 'descendant' },
      expandAndCollapse: true,
      data: [
        {
          name: 'App',
          children: [
            { name: 'Pages', children: [
              { name: 'PageA', children: [{ name: 'ComponentX' }, { name: 'ComponentY' }] },
              { name: 'PageB', children: [{ name: 'ComponentW' }] }
            ]},
            { name: 'Shared', children: [{ name: 'ComponentX' }, { name: 'ComponentZ' }] },
            { name: 'Utils', children: [{ name: 'Helpers' }] }
          ]
        }
      ]
    }
  ]
};
```
