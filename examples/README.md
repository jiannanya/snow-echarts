# ECharts Examples — Index

> 2-3 working, copy-paste `option` objects for every ECharts chart type.  
> Each file targets the standard `chart.setOption(option)` API.

---

## Core Charts

| File | Chart Types | Examples |
|------|-------------|----------|
| [bar.md](./bar.md) | Bar, Grouped Bar, Horizontal Bar | Grouped with labels; Population pyramid; Bar race |
| [line.md](./line.md) | Line, Area | Smooth area + markLine; Gradient stacked area; Dual Y-axis |
| [pie.md](./pie.md) | Pie, Doughnut, Rose | Doughnut KPI; Nightingale rose; Nested double-pie |
| [scatter.md](./scatter.md) | Scatter, Bubble, EffectScatter | GDP bubble; Ripple effect; Regression trend line |

---

## Financial & Scientific

| File | Chart Types | Examples |
|------|-------------|----------|
| [candlestick.md](./candlestick.md) | Candlestick, OHLC | Basic + volume subplot; MA + Bollinger; Brush + dataZoom |
| [boxplot.md](./boxplot.md) | Boxplot | Boxplot + outliers; Multi-category; Horizontal + auto-quartiles |
| [heatmap.md](./heatmap.md) | Heatmap (cartesian) | Commit activity; Calendar heatmap; Correlation matrix |
| [radar.md](./radar.md) | Radar | Product comparison; AQI radar; Skills vs target |

---

## Geographic

| File | Chart Types | Examples |
|------|-------------|----------|
| [map.md](./map.md) | Map, Geo, Lines | World choropleth; Scatter on geo; Animated flight routes |

---

## Hierarchical

| File | Chart Types | Examples |
|------|-------------|----------|
| [tree.md](./tree.md) | Tree | Collapsible org chart; Radial file system; Side-by-side trees |
| [treemap.md](./treemap.md) | Treemap | Breadcrumb treemap; Colored by metric; Drill-down |
| [sunburst.md](./sunburst.md) | Sunburst | Budget drill-down; visualMap coloring; Dark monochrome |

---

## Flow & Relationship

| File | Chart Types | Examples |
|------|-------------|----------|
| [graph.md](./graph.md) | Graph (Force, Circular) | Force network; Circular team; Graph on cartesian |
| [sankey.md](./sankey.md) | Sankey | Energy flow; Customer journey; Budget allocation |
| [parallel.md](./parallel.md) | Parallel Coordinates | AQI 10 cities; Cars with brush; Stock portfolio |
| [chord.md](./chord.md) | Chord *(v6+)* | Global trade; Gradient team edges; Language influence |

---

## Special Charts

| File | Chart Types | Examples |
|------|-------------|----------|
| [funnel.md](./funnel.md) | Funnel, Pyramid | Sales conversion; Actual vs Target; Maslow pyramid |
| [gauge.md](./gauge.md) | Gauge | KPI gauge with zones; Multi-ring progress; Live animated gauge |
| [pictorialbar.md](./pictorialbar.md) | PictorialBar | Repeating icons; Staged capacity; Body-fill water level |
| [themeriver-calendar.md](./themeriver-calendar.md) | ThemeRiver, Calendar | Language topic stream; Music genre trends; GitHub activity; Calendar + events |

---

## Modern / Utility

| File | Chart Types | Examples |
|------|-------------|----------|
| [custom.md](./custom.md) | Custom (renderItem) | Gantt chart; Error bars on scatter; Hour×Day heatmap |
| [dataset-datazoom.md](./dataset-datazoom.md) | Dataset, DataZoom | Multi-series dataset; Dataset transforms; Slider+inside zoom |

---

## 3D Charts (echarts-gl)

| File | Chart Types | Examples |
|------|-------------|----------|
| [3d-gl.md](./3d-gl.md) | bar3D, scatter3D, lines3D, Globe | 3D bar grid; 3D health scatter; Globe flight routes |

> **Note**: All 3D examples require [echarts-gl](https://github.com/ecomfe/echarts-gl).  
> `npm install echarts-gl` then `import 'echarts-gl'` alongside echarts.

---

## Quick Start

```js
// 1. Init
const chart = echarts.init(document.getElementById('chart'));

// 2. Paste any option from the files above
const option = { /* ... */ };

// 3. Apply
chart.setOption(option);
```

## Chart Type → File Mapping

| ECharts `type` | File |
|----------------|------|
| `'bar'` | [bar.md](./bar.md) |
| `'line'` | [line.md](./line.md) |
| `'pie'` | [pie.md](./pie.md) |
| `'scatter'`, `'effectScatter'` | [scatter.md](./scatter.md) |
| `'candlestick'` | [candlestick.md](./candlestick.md) |
| `'boxplot'` | [boxplot.md](./boxplot.md) |
| `'heatmap'` | [heatmap.md](./heatmap.md) |
| `'radar'` | [radar.md](./radar.md) |
| `'map'`, `'lines'` | [map.md](./map.md) |
| `'tree'` | [tree.md](./tree.md) |
| `'treemap'` | [treemap.md](./treemap.md) |
| `'sunburst'` | [sunburst.md](./sunburst.md) |
| `'graph'` | [graph.md](./graph.md) |
| `'sankey'` | [sankey.md](./sankey.md) |
| `'parallel'` | [parallel.md](./parallel.md) |
| `'chord'` *(v6+)* | [chord.md](./chord.md) |
| `'funnel'` | [funnel.md](./funnel.md) |
| `'gauge'` | [gauge.md](./gauge.md) |
| `'pictorialBar'` | [pictorialbar.md](./pictorialbar.md) |
| `'themeRiver'` | [themeriver-calendar.md](./themeriver-calendar.md) |
| `coordinateSystem: 'calendar'` | [themeriver-calendar.md](./themeriver-calendar.md) |
| `'custom'` | [custom.md](./custom.md) |
| `dataset`, `transform` | [dataset-datazoom.md](./dataset-datazoom.md) |
| `dataZoom` | [dataset-datazoom.md](./dataset-datazoom.md) |
| `'bar3D'`, `'scatter3D'`, `'lines3D'` | [3d-gl.md](./3d-gl.md) |
