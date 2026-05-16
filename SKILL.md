---
name: echarts
description: "Create, configure, and customize Apache ECharts charts and visualizations. Use when: building charts with ECharts; selecting chart types (bar, line, pie, scatter, map, heatmap, radar, candlestick, funnel, gauge, tree, treemap, sankey, graph, boxplot, pictorialBar, themeRiver, sunburst, parallel, calendar, custom, matrix, chord, 3D/GL charts); configuring series, axes, legends, tooltips, dataZoom, visualMap, toolbox; using echarts.init, setOption, on/off events; implementing responsive charts; theme customization; large-data rendering optimization. Covers all chart types from the official examples gallery including v6 Matrix/Chord and echarts-gl 3D charts."
argument-hint: "Describe the chart you want (e.g., 'bar chart comparing monthly sales', 'heatmap for correlation matrix')"
---

# Apache ECharts Skill

## Overview

Apache ECharts (https://echarts.apache.org) is a powerful, interactive, open-source visualization library built in JavaScript. It uses a declarative `option` object passed to `chart.setOption()`.

## When to Use This Skill

- Creating any chart with ECharts (bar, line, pie, scatter, map, etc.)
- Configuring axes, legends, tooltips, data zoom, visual maps
- Handling ECharts events and interactions
- Optimizing performance for large datasets
- Customizing themes and styles
- Server-side rendering or React/Vue integration

---

## Core Concept: The Option Object

Every ECharts chart is driven by a single configuration object:

```js
const option = {
  title:      { text: 'Chart Title' },
  tooltip:    { trigger: 'axis' },
  legend:     { data: ['Series A'] },
  xAxis:      { type: 'category', data: ['Mon','Tue','Wed'] },
  yAxis:      { type: 'value' },
  series:     [{ name: 'Series A', type: 'bar', data: [120, 200, 150] }]
};
chart.setOption(option);
```

Key top-level properties:

| Property | Purpose |
|---|---|
| `title` | Chart title & subtitle |
| `legend` | Toggle series visibility |
| `grid` | Cartesian coordinate layout |
| `xAxis` / `yAxis` | Axis config for cartesian charts |
| `polar` / `radiusAxis` / `angleAxis` | Polar coordinate axes |
| `radar` | Radar chart indicator config |
| `tooltip` | Hover tooltip behavior |
| `toolbox` | Built-in tools (save image, zoom, data view) |
| `dataZoom` | Scroll/slider zoom on axes |
| `visualMap` | Data-to-color/size mapping |
| `series` | **Array** of data series — each has a `type` |
| `dataset` | Shared data source (alternative to inline data) |
| `color` | Global color palette array |
| `backgroundColor` | Canvas background color |
| `animation` | Boolean; toggle animations |

---

## Quick Start

### 1. Install
```bash
npm install echarts
```

### 2. Basic HTML usage
```html
<div id="chart" style="width:600px;height:400px;"></div>
<script src="https://cdn.jsdelivr.net/npm/echarts/dist/echarts.min.js"></script>
<script>
  const chart = echarts.init(document.getElementById('chart'));
  chart.setOption({ /* option */ });
</script>
```

### 3. ES module (tree-shaking)
```js
import * as echarts from 'echarts/core';
import { BarChart } from 'echarts/charts';
import { GridComponent, TooltipComponent, LegendComponent } from 'echarts/components';
import { CanvasRenderer } from 'echarts/renderers';

echarts.use([BarChart, GridComponent, TooltipComponent, LegendComponent, CanvasRenderer]);

const chart = echarts.init(document.getElementById('chart'));
chart.setOption(option);
```

---

## Procedure for Building a Chart

1. **Choose chart type** → See [Chart Types Reference](./references/chart-types.md)
2. **Prepare data** — inline in `series.data`, or use `dataset`
3. **Build the option object** → See [Options Reference](./references/options-reference.md)
4. **Initialize & render**:
   ```js
   const chart = echarts.init(dom, theme, { renderer: 'canvas' });
   chart.setOption(option);
   ```
5. **Handle resize**:
   ```js
   window.addEventListener('resize', () => chart.resize());
   ```
6. **Bind events** (optional):
   ```js
   chart.on('click', (params) => console.log(params));
   ```

→ See [Code Templates](./assets/templates.md) for copy-paste examples of all major chart types.  
→ See [Examples by Chart Type](./examples/README.md) for 2-3 detailed working examples per chart type.

---

## Selecting the Right Chart Type

| Data Pattern | Recommended Chart |
|---|---|
| Comparisons across categories | `bar` |
| Trend over time | `line` |
| Part-to-whole / proportion | `pie`, `sunburst` |
| Correlation between two measures | `scatter` |
| Distribution (x=value, y=freq) | `bar` with binned data |
| Hierarchical structure | `tree`, `treemap` |
| Flow between nodes | `sankey`, `graph` |
| Geographic data | `map`, `scatter` on geo |
| Multi-dimensional | `radar`, `parallel` |
| OHLC financial | `candlestick` |
| Density over 2D grid | `heatmap` |
| Progress / KPI | `gauge`, `liquidFill` |
| Time-range data | `calendar` heatmap |

---

## API Quick Reference

```js
// Init
const chart = echarts.init(dom, theme?, opts?);
// opts: { renderer: 'canvas'|'svg', width, height, devicePixelRatio, locale }

// Set options (merges by default)
chart.setOption(option, notMerge?, lazyUpdate?);

// Resize chart (call on window resize)
chart.resize({ width?, height? });

// Event binding
chart.on(eventName, handler);   // 'click', 'mouseover', 'datazoom', 'legendselectchanged', etc.
chart.off(eventName, handler);

// Programmatic highlight
chart.dispatchAction({ type: 'highlight', seriesIndex: 0, dataIndex: 2 });

// Convert data coords to pixel
chart.convertToPixel({ seriesIndex: 0 }, [xVal, yVal]);

// Export image
const url = chart.getDataURL({ type: 'png', pixelRatio: 2, backgroundColor: '#fff' });

// Destroy instance
chart.dispose();

// Utilities
echarts.registerTheme('myTheme', themeObj);
echarts.registerMap('mapName', { geoJSON });
echarts.connect([chart1, chart2]);  // sync interactions
```

---

## Common Patterns

### Responsive resize
```js
const observer = new ResizeObserver(() => chart.resize());
observer.observe(dom);
```

### Dynamic data update
```js
chart.setOption({ series: [{ data: newData }] });
// For performance with large data:
chart.setOption({ series: [{ data: newData }] }, false, true); // lazyUpdate
```

### Loading indicator
```js
chart.showLoading();
fetch('/api/data').then(r => r.json()).then(data => {
  chart.hideLoading();
  chart.setOption(buildOption(data));
});
```

### Tooltip formatter
```js
tooltip: {
  formatter: (params) => {
    if (Array.isArray(params)) {
      return params.map(p => `${p.marker}${p.seriesName}: ${p.value}`).join('<br/>');
    }
    return `${params.name}: ${params.value}`;
  }
}
```

### Large data optimization
```js
series: [{
  type: 'line',
  data: bigArray,
  sampling: 'lttb',      // downsample large series
  large: true,           // scatter: enable large mode
  largeThreshold: 2000,
  progressive: 200,      // render progressively
  animation: false
}]
```

---

## References

- [Chart Types Reference](./references/chart-types.md) — all series types with key options
- [Options Reference](./references/options-reference.md) — components (tooltip, legend, dataZoom, etc.)
- [Code Templates](./assets/templates.md) — complete copy-paste examples
- [Official Examples](./assets/official-examples.md) — examples sourced directly from echarts.apache.org/examples
- [Examples by Chart Type](./examples/README.md) — 2-3 working copy-paste `option` objects for every chart type
- [Demo Portal](./assets/demo.html) — embeds the official examples gallery; falls back to a launch page with direct links
- Official docs: https://echarts.apache.org/en/option.html
- Official API: https://echarts.apache.org/en/api.html
- Examples gallery: https://echarts.apache.org/examples/en/index.html
