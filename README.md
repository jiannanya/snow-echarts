<div align="right">
  🌐 &nbsp;<strong>English</strong> &nbsp;|&nbsp; <a href="./README.zh.md">中文</a>
</div>

---

# snow-echarts AI Skill

> The snow-echarts skill generates complete, production-ready **Apache ECharts** configurations from natural-language descriptions.  
> Covers every chart type in the official gallery, all configuration components, and framework integrations for React, Vue, and plain JS.

[![ECharts](https://img.shields.io/badge/Apache%20ECharts-v5%2B-blue?logo=apache)](https://echarts.apache.org)
[![echarts-gl](https://img.shields.io/badge/echarts--gl-v2-orange)](https://github.com/ecomfe/echarts-gl)
[![License](https://img.shields.io/badge/license-MIT-green)](../../LICENSE)

---

## 🖼️ Example Gallery

> Live interactive gallery → **[Open examples.html](./examples.html)** in your browser  
> All chart types with live rendering, code toggle, and sidebar navigation.

<table>
<tr>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=bar-label-rotation">
    <img src="https://echarts.apache.org/examples/data/thumb/bar-label-rotation.webp" width="180" alt="Bar Chart"/>
  </a>
  <br/><sub><b>Bar Chart</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=line-smooth">
    <img src="https://echarts.apache.org/examples/data/thumb/line-smooth.webp" width="180" alt="Line Chart"/>
  </a>
  <br/><sub><b>Line / Area</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=pie-doughnut">
    <img src="https://echarts.apache.org/examples/data/thumb/pie-doughnut.webp" width="180" alt="Pie / Doughnut"/>
  </a>
  <br/><sub><b>Pie / Doughnut</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=scatter-simple">
    <img src="https://echarts.apache.org/examples/data/thumb/scatter-simple.webp" width="180" alt="Scatter"/>
  </a>
  <br/><sub><b>Scatter / Bubble</b></sub>
</td>
</tr>
<tr>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=heatmap-cartesian">
    <img src="https://echarts.apache.org/examples/data/thumb/heatmap-cartesian.webp" width="180" alt="Heatmap"/>
  </a>
  <br/><sub><b>Heatmap</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=radar-aqi">
    <img src="https://echarts.apache.org/examples/data/thumb/radar-aqi.webp" width="180" alt="Radar"/>
  </a>
  <br/><sub><b>Radar</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=sankey-energy">
    <img src="https://echarts.apache.org/examples/data/thumb/sankey-energy.webp" width="180" alt="Sankey"/>
  </a>
  <br/><sub><b>Sankey Flow</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=graph-force">
    <img src="https://echarts.apache.org/examples/data/thumb/graph-force.webp" width="180" alt="Graph"/>
  </a>
  <br/><sub><b>Graph / Network</b></sub>
</td>
</tr>
<tr>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=candlestick-sh">
    <img src="https://echarts.apache.org/examples/data/thumb/candlestick-sh.webp" width="180" alt="Candlestick"/>
  </a>
  <br/><sub><b>Candlestick (OHLC)</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=gauge-progress">
    <img src="https://echarts.apache.org/examples/data/thumb/gauge-progress.webp" width="180" alt="Gauge"/>
  </a>
  <br/><sub><b>Gauge / KPI</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=treemap-disk">
    <img src="https://echarts.apache.org/examples/data/thumb/treemap-disk.webp" width="180" alt="Treemap"/>
  </a>
  <br/><sub><b>Treemap</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=bar3d-with-surface&gl=1">
    <img src="https://echarts.apache.org/examples/data/thumb/bar3d-with-surface.webp" width="180" alt="3D Bar"/>
  </a>
  <br/><sub><b>3D Charts (echarts-gl)</b></sub>
</td>
</tr>
</table>

> Click any thumbnail to open it in the ECharts live editor.

---

## ✨ What This Skill Does

When invoked, this skill instructs Agent to:

- **Generate complete `option` objects** — ready to drop into `chart.setOption()`
- **Select the right chart type** for your data and use case automatically
- **Configure all components** — axes, legends, tooltips, dataZoom, visualMap, toolbox
- **Handle framework integration** — React hooks, Vue 3 composables, tree-shaking imports
- **Apply visual polish** — gradients, custom colors, responsive layout, animations
- **Optimize for scale** — `large` mode, `sampling`, `progressive` rendering for big datasets
- **Support 3D charts** via `echarts-gl` (bar3D, scatter3D, globe, surface)
- **Cover every chart type** in the official gallery, including v6 Chord and Matrix

---

## 📊 Chart Types Covered

### Core Charts

| Type | Series Name | Key Use Cases |
|------|-------------|---------------|
| Bar | `bar` | Category comparison, ranking, waterfall, race |
| Line | `line` | Trends over time, area charts, step charts |
| Pie | `pie` | Part-to-whole, doughnut, nightingale rose |
| Scatter | `scatter`, `effectScatter` | Correlation, bubble charts, ripple effects |

### Financial & Scientific

| Type | Series Name | Key Use Cases |
|------|-------------|---------------|
| Candlestick | `candlestick` | Stock OHLC data, financial charts |
| Boxplot | `boxplot` | Statistical distributions, outlier detection |
| Heatmap | `heatmap` | 2D density, calendar activity, correlation matrix |
| Radar | `radar` | Multi-dimensional comparison |

### Geographic

| Type | Series Name | Key Use Cases |
|------|-------------|---------------|
| Map | `map` | Choropleth, regional data |
| Geo | `geo` | Background map layer for overlays |
| Lines | `lines` | Flight routes, migration flows on maps |

### Hierarchical

| Type | Series Name | Key Use Cases |
|------|-------------|---------------|
| Tree | `tree` | Org charts, file systems, collapsible hierarchy |
| Treemap | `treemap` | Hierarchical area, disk usage, portfolio |
| Sunburst | `sunburst` | Multi-level drill-down pie |

### Flow & Relationship

| Type | Series Name | Key Use Cases |
|------|-------------|---------------|
| Graph | `graph` | Force-directed networks, circular layout |
| Sankey | `sankey` | Energy flows, user journeys, budget allocation |
| Parallel | `parallel` | Multi-dimensional data exploration |
| Chord | `chord` *(v6+)* | Circular flow, global trade, relationships |

### Special Charts

| Type | Series Name | Key Use Cases |
|------|-------------|---------------|
| Funnel | `funnel` | Conversion funnels, sales pipeline |
| Gauge | `gauge` | KPI dashboards, speedometers, progress rings |
| PictorialBar | `pictorialBar` | Infographic-style icon bars |
| ThemeRiver | `themeRiver` | Topic/category evolution over time |
| Calendar | `heatmap` on `calendar` | Activity calendars (GitHub-style) |

### Modern / Utility

| Type | Series Name | Key Use Cases |
|------|-------------|---------------|
| Custom | `custom` | Gantt charts, error bars, any shape via `renderItem` |
| Dataset | `dataset` | Shared data source, data transforms, filtering |
| DataZoom | *(component)* | Scroll/slider zoom on time-series data |

### 3D Charts *(echarts-gl required)*

| Type | Series Name | Key Use Cases |
|------|-------------|---------------|
| 3D Bar | `bar3D` | 3-axis bar grids |
| 3D Scatter | `scatter3D` | Point clouds, 3D clustering |
| 3D Lines | `lines3D` | 3D trajectories |
| Surface | `surface` | Mathematical surfaces, terrain |
| Globe | `globe` | Spherical earth with data overlays |

---

## 🚀 Quick Start

### 1. Install ECharts

```bash
# npm
npm install echarts

# CDN (HTML)
<script src="https://cdn.jsdelivr.net/npm/echarts@5/dist/echarts.min.js"></script>

# For 3D charts, also add:
npm install echarts-gl
```

### 2. Basic Usage

```html
<div id="chart" style="width: 600px; height: 400px;"></div>
<script src="https://cdn.jsdelivr.net/npm/echarts@5/dist/echarts.min.js"></script>
<script>
  const chart = echarts.init(document.getElementById('chart'));
  chart.setOption({
    title:  { text: 'Monthly Sales' },
    tooltip: { trigger: 'axis' },
    xAxis:  { type: 'category', data: ['Jan','Feb','Mar','Apr','May','Jun'] },
    yAxis:  { type: 'value' },
    series: [{ type: 'bar', data: [120, 200, 150, 80, 70, 110] }]
  });
  window.addEventListener('resize', () => chart.resize());
</script>
```

### 3. React (with tree-shaking)

```jsx
import { useEffect, useRef } from 'react';
import * as echarts from 'echarts/core';
import { BarChart } from 'echarts/charts';
import { GridComponent, TooltipComponent, LegendComponent } from 'echarts/components';
import { CanvasRenderer } from 'echarts/renderers';

echarts.use([BarChart, GridComponent, TooltipComponent, LegendComponent, CanvasRenderer]);

export function Chart({ option }) {
  const ref = useRef(null);
  const chartRef = useRef(null);

  useEffect(() => {
    chartRef.current = echarts.init(ref.current);
    const ro = new ResizeObserver(() => chartRef.current?.resize());
    ro.observe(ref.current);
    return () => { ro.disconnect(); chartRef.current?.dispose(); };
  }, []);

  useEffect(() => { chartRef.current?.setOption(option, true); }, [option]);

  return <div ref={ref} style={{ width: '100%', height: 400 }} />;
}
```

### 4. Vue 3

```vue
<template>
  <div ref="el" style="width: 100%; height: 400px" />
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from 'vue';
import * as echarts from 'echarts';

const props = defineProps({ option: Object });
const el = ref(null);
let chart;

onMounted(() => {
  chart = echarts.init(el.value);
  chart.setOption(props.option);
  window.addEventListener('resize', () => chart.resize());
});
watch(() => props.option, (opt) => chart?.setOption(opt, true), { deep: true });
onBeforeUnmount(() => { chart?.dispose(); });
</script>
```

---

## 📁 File Structure

```
skills/echarts/
├── README.md                   # ← You are here (English)
├── README.zh.md                # Chinese version
├── SKILL.md                    # Main skill definition (loaded by Agent)
├── examples.html               # 🌐 Live interactive gallery (open in browser)
│
├── assets/
│   ├── templates.md            # Framework integration patterns (React, Vue, tree-shaking)
│   └── official-examples.md   # Complete catalog of official ECharts examples with links
│
├── examples/                   # 2-3 complete working option objects per chart type
│   ├── README.md               # Examples index with navigation table
│   ├── bar.md                  # Bar chart examples
│   ├── line.md                 # Line / Area chart examples
│   ├── pie.md                  # Pie / Doughnut / Rose examples
│   ├── scatter.md              # Scatter / Bubble / EffectScatter
│   ├── candlestick.md          # OHLC + volume + indicators
│   ├── boxplot.md              # Statistical box plots
│   ├── heatmap.md              # Cartesian + Calendar heatmaps
│   ├── radar.md                # Radar / Spider charts
│   ├── map.md                  # Choropleth + Geo + Lines
│   ├── tree.md                 # Collapsible tree / org chart
│   ├── treemap.md              # Hierarchical area charts
│   ├── sunburst.md             # Multi-level drill-down
│   ├── graph.md                # Force-directed network / circular
│   ├── sankey.md               # Flow / energy diagrams
│   ├── parallel.md             # Parallel coordinate axes
│   ├── chord.md                # Chord diagrams (v6+)
│   ├── funnel.md               # Conversion funnels
│   ├── gauge.md                # KPI gauges / progress rings
│   ├── pictorialbar.md         # Icon-based pictorial bars
│   ├── themeriver-calendar.md  # ThemeRiver streams + Calendar
│   ├── custom.md               # Custom renderItem series
│   ├── dataset-datazoom.md     # Dataset transforms + DataZoom
│   ├── mixed-realtime.md       # Mixed chart types + live updates
│   └── 3d-gl.md               # 3D charts (echarts-gl)
│
└── references/
    ├── chart-types.md          # All series types with key options
    └── options-reference.md   # All components (tooltip, legend, dataZoom…)
```

---

## ⚙️ How the Skill Works


### Invocation

The skill is automatically triggered when your prompt involves ECharts charting. The `description` in `SKILL.md` drives semantic matching:

```yaml
name: snow-echarts
description: "Create, configure, and customize Apache ECharts charts..."
argument-hint: "Describe the chart you want (e.g., 'bar chart comparing monthly sales')"
```

### What gets generated

Agent will produce a complete, self-contained `option` object:

```js
// Example: "Create a dual Y-axis chart showing rainfall and temperature"
const option = {
  tooltip: { trigger: 'axis', axisPointer: { type: 'cross' } },
  legend: { data: ['Rainfall', 'Temperature'] },
  xAxis: [{ type: 'category', data: ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'] }],
  yAxis: [
    { type: 'value', name: 'Rainfall', axisLabel: { formatter: '{value} ml' } },
    { type: 'value', name: 'Temperature', position: 'right', axisLabel: { formatter: '{value} °C' } }
  ],
  series: [
    { name: 'Rainfall', type: 'bar', data: [2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3] },
    { name: 'Temperature', type: 'line', yAxisIndex: 1, data: [2.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2] }
  ]
};
```

---

## 🔑 Key Concepts

### The Option Object

Every ECharts chart is driven by a single declarative configuration object:

| Top-level Key | Purpose |
|---------------|---------|
| `title` | Chart title and subtitle |
| `legend` | Series toggle controls |
| `grid` | Cartesian coordinate layout (margins) |
| `xAxis` / `yAxis` | Axis configuration for cartesian charts |
| `polar` / `radiusAxis` / `angleAxis` | Polar coordinate axes |
| `radar` | Radar indicator configuration |
| `geo` | Geographic background layer |
| `tooltip` | Hover tooltip behavior |
| `toolbox` | Built-in tools (save image, data view, zoom) |
| `dataZoom` | Scroll and slider zoom components |
| `visualMap` | Data → color/size mapping |
| `series` | **Array** of data series — each has `type`, `data`, `name` |
| `dataset` | Shared data source (alternative to inline `data`) |
| `color` | Global color palette array |
| `backgroundColor` | Canvas background color |
| `animation` | Enable/disable animations |

### Useful API Methods

```js
const chart = echarts.init(dom, theme?, opts?);
chart.setOption(option, notMerge?, lazyUpdate?);
chart.resize({ width?, height? });
chart.on('click', params => { /* handler */ });
chart.off('click', handler);
chart.dispatchAction({ type: 'highlight', seriesIndex: 0, dataIndex: 2 });
chart.getDataURL({ type: 'png', pixelRatio: 2 });
chart.dispose();
echarts.registerTheme('name', themeObj);
echarts.registerMap('name', geoJSON);
echarts.connect([chart1, chart2]);  // sync interactions across charts
```

### Performance Tips for Large Data

```js
series: [{
  type: 'line',
  data: bigArray,          // 10k+ points
  sampling: 'lttb',        // Largest-Triangle-Three-Buckets downsampling
  large: true,             // scatter: GPU-accelerated large mode
  largeThreshold: 2000,
  progressive: 200,        // render 200 points per frame
  animation: false         // disable animation for large data
}]
```

---

## 📚 Resources

| Resource | Description |
|----------|-------------|
| [examples.html](./examples.html) | **Live gallery** — 30 charts with code toggle (open in browser) |
| [SKILL.md](./SKILL.md) | Main skill definition loaded by Agent |
| [examples/README.md](./examples/README.md) | Index of all 25 example files (2-3 options each) |
| [assets/templates.md](./assets/templates.md) | React, Vue, tree-shaking integration patterns |
| [assets/official-examples.md](./assets/official-examples.md) | Links to all official ECharts examples by type |
| [references/chart-types.md](./references/chart-types.md) | All series types with key configuration options |
| [references/options-reference.md](./references/options-reference.md) | All components reference (tooltip, legend, dataZoom…) |
| [Official Docs](https://echarts.apache.org/en/option.html) | Complete ECharts option documentation |
| [Official API](https://echarts.apache.org/en/api.html) | ECharts instance API reference |
| [Examples Gallery](https://echarts.apache.org/examples/en/index.html) | 400+ official interactive examples |
