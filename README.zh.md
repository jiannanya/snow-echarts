<div align="right">
  🌐 &nbsp;<a href="./README.md">English</a> &nbsp;|&nbsp; <strong>中文</strong>
</div>

---

# Apache ECharts — GitHub Copilot AI 技能

> 一套完整的 GitHub Copilot 技能，可根据自然语言描述，生成即用型 **Apache ECharts** 配置。  
> 覆盖官方示例库中的所有图表类型、所有配置组件，以及 React、Vue、原生 JS 的框架集成方案。

[![ECharts](https://img.shields.io/badge/Apache%20ECharts-v5%2B-blue?logo=apache)](https://echarts.apache.org)
[![echarts-gl](https://img.shields.io/badge/echarts--gl-v2-orange)](https://github.com/ecomfe/echarts-gl)
[![License](https://img.shields.io/badge/license-MIT-green)](../../LICENSE)

---

## 🖼️ 示例预览

> 在线交互式图表库 → 用浏览器打开 **[examples.html](./examples.html)**  
> 包含所有图表类型的实时渲染、代码切换功能和侧边栏导航。

<table>
<tr>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=bar-label-rotation">
    <img src="https://echarts.apache.org/examples/data/thumb/bar-label-rotation.webp" width="180" alt="柱状图"/>
  </a>
  <br/><sub><b>柱状图</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=line-smooth">
    <img src="https://echarts.apache.org/examples/data/thumb/line-smooth.webp" width="180" alt="折线图"/>
  </a>
  <br/><sub><b>折线图 / 面积图</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=pie-doughnut">
    <img src="https://echarts.apache.org/examples/data/thumb/pie-doughnut.webp" width="180" alt="饼图"/>
  </a>
  <br/><sub><b>饼图 / 环形图</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=scatter-simple">
    <img src="https://echarts.apache.org/examples/data/thumb/scatter-simple.webp" width="180" alt="散点图"/>
  </a>
  <br/><sub><b>散点图 / 气泡图</b></sub>
</td>
</tr>
<tr>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=heatmap-cartesian">
    <img src="https://echarts.apache.org/examples/data/thumb/heatmap-cartesian.webp" width="180" alt="热力图"/>
  </a>
  <br/><sub><b>热力图</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=radar-aqi">
    <img src="https://echarts.apache.org/examples/data/thumb/radar-aqi.webp" width="180" alt="雷达图"/>
  </a>
  <br/><sub><b>雷达图</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=sankey-energy">
    <img src="https://echarts.apache.org/examples/data/thumb/sankey-energy.webp" width="180" alt="桑基图"/>
  </a>
  <br/><sub><b>桑基图（能量流）</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=graph-force">
    <img src="https://echarts.apache.org/examples/data/thumb/graph-force.webp" width="180" alt="关系图"/>
  </a>
  <br/><sub><b>关系图 / 网络图</b></sub>
</td>
</tr>
<tr>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=candlestick-sh">
    <img src="https://echarts.apache.org/examples/data/thumb/candlestick-sh.webp" width="180" alt="K线图"/>
  </a>
  <br/><sub><b>K线图（OHLC）</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=gauge-progress">
    <img src="https://echarts.apache.org/examples/data/thumb/gauge-progress.webp" width="180" alt="仪表盘"/>
  </a>
  <br/><sub><b>仪表盘 / KPI</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=treemap-disk">
    <img src="https://echarts.apache.org/examples/data/thumb/treemap-disk.webp" width="180" alt="矩形树图"/>
  </a>
  <br/><sub><b>矩形树图</b></sub>
</td>
<td align="center" width="200">
  <a href="https://echarts.apache.org/examples/en/editor.html?c=bar3d-with-surface&gl=1">
    <img src="https://echarts.apache.org/examples/data/thumb/bar3d-with-surface.webp" width="180" alt="3D图表"/>
  </a>
  <br/><sub><b>3D 图表（echarts-gl）</b></sub>
</td>
</tr>
</table>

> 点击任意缩略图，可在 ECharts 在线编辑器中查看完整代码。

---

## ✨ 技能功能

调用本技能后，Copilot 将：

- **生成完整的 `option` 配置对象** — 可直接传入 `chart.setOption()`，开箱即用
- **自动选择最合适的图表类型** — 根据你的数据特征和使用场景智能判断
- **配置所有组件** — 坐标轴、图例、提示框、dataZoom、visualMap、工具栏等
- **处理框架集成** — React Hooks、Vue 3 Composable、tree-shaking 按需导入
- **美化视觉效果** — 渐变色、自定义调色板、响应式布局、入场动画
- **大数据优化** — `large` 模式、`sampling` 采样、`progressive` 渐进渲染
- **支持 3D 图表** — 通过 `echarts-gl` 实现 bar3D、scatter3D、Globe、曲面图
- **覆盖所有官方图表类型** — 包括 v6 版本的 Chord、Matrix 等新增类型

---

## 📊 支持的图表类型

### 基础图表

| 类型 | 系列名 | 典型场景 |
|------|--------|----------|
| 柱状图 | `bar` | 分类对比、排名、瀑布图、动态排序 |
| 折线图 | `line` | 时间趋势、面积图、阶梯图 |
| 饼图 | `pie` | 占比分析、环形图、玫瑰图 |
| 散点图 | `scatter`、`effectScatter` | 相关性分析、气泡图、涟漪动效 |

### 金融 & 统计

| 类型 | 系列名 | 典型场景 |
|------|--------|----------|
| K线图 | `candlestick` | 股票 OHLC 数据、金融走势 |
| 箱形图 | `boxplot` | 统计分布、异常值检测 |
| 热力图 | `heatmap` | 二维密度、日历活跃度、相关矩阵 |
| 雷达图 | `radar` | 多维度对比 |

### 地理图表

| 类型 | 系列名 | 典型场景 |
|------|--------|----------|
| 地图 | `map` | 区域着色图（Choropleth） |
| 地理坐标 | `geo` | 地图背景层（可叠加散点/线条） |
| 线图（地理） | `lines` | 飞线图、迁徙流向图 |

### 层次结构

| 类型 | 系列名 | 典型场景 |
|------|--------|----------|
| 树图 | `tree` | 组织架构、文件系统、可折叠层级 |
| 矩形树图 | `treemap` | 层级面积图、磁盘占用分析 |
| 旭日图 | `sunburst` | 多层级占比钻取 |

### 流向 & 关系

| 类型 | 系列名 | 典型场景 |
|------|--------|----------|
| 关系图 | `graph` | 力导向网络、环形布局 |
| 桑基图 | `sankey` | 能量流、用户路径、预算流向 |
| 平行坐标 | `parallel` | 多维数据探索 |
| 弦图 | `chord` *(v6+)* | 圆形流量、贸易关系、相互影响 |

### 特殊图表

| 类型 | 系列名 | 典型场景 |
|------|--------|----------|
| 漏斗图 | `funnel` | 转化率漏斗、销售管道 |
| 仪表盘 | `gauge` | KPI 面板、进度环、速度表 |
| 象形柱图 | `pictorialBar` | 信息图风格的图标柱 |
| 主题河流图 | `themeRiver` | 主题/类别随时间的演变 |
| 日历图 | `calendar` 上的 `heatmap` | GitHub 风格活跃度日历 |

### 现代 & 工具类

| 类型 | 系列名 | 典型场景 |
|------|--------|----------|
| 自定义系列 | `custom` | 甘特图、误差棒、任意形状 |
| 数据集 | `dataset` | 共享数据源、数据变换与过滤 |
| 数据缩放 | *(组件)* | 时序数据的滑动/滚轮缩放 |

### 3D 图表 *(需要 echarts-gl)*

| 类型 | 系列名 | 典型场景 |
|------|--------|----------|
| 3D 柱状图 | `bar3D` | 三轴柱状网格 |
| 3D 散点图 | `scatter3D` | 点云、三维聚类 |
| 3D 曲面图 | `surface` | 数学曲面、地形图 |
| 地球 | `globe` | 球形地球 + 数据叠加 |

---

## 🚀 快速开始

### 1. 安装

```bash
# npm
npm install echarts

# CDN（HTML 直接引用）
<script src="https://cdn.jsdelivr.net/npm/echarts@5/dist/echarts.min.js"></script>

# 3D 图表还需要：
npm install echarts-gl
```

### 2. 基础用法

```html
<div id="chart" style="width: 600px; height: 400px;"></div>
<script src="https://cdn.jsdelivr.net/npm/echarts@5/dist/echarts.min.js"></script>
<script>
  const chart = echarts.init(document.getElementById('chart'));
  chart.setOption({
    title:  { text: '月度销售额' },
    tooltip: { trigger: 'axis' },
    xAxis:  { type: 'category', data: ['1月','2月','3月','4月','5月','6月'] },
    yAxis:  { type: 'value' },
    series: [{ type: 'bar', data: [120, 200, 150, 80, 70, 110] }]
  });
  window.addEventListener('resize', () => chart.resize());
</script>
```

### 3. React 集成（含 tree-shaking）

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

### 4. Vue 3 集成

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

## 📁 文件结构

```
.github/skills/echarts/
├── README.md                   # 英文版说明（English）
├── README.zh.md                # ← 当前文件（中文）
├── SKILL.md                    # 技能主定义文件（由 Copilot 加载）
├── examples.html               # 🌐 在线交互式图表库（浏览器打开）
│
├── assets/
│   ├── templates.md            # 框架集成模板（React、Vue、tree-shaking）
│   └── official-examples.md   # 官方示例完整目录（含链接）
│
├── examples/                   # 每种图表类型 2-3 个完整 option 示例
│   ├── README.md               # 示例索引（导航表格）
│   ├── bar.md                  # 柱状图示例
│   ├── line.md                 # 折线图 / 面积图示例
│   ├── pie.md                  # 饼图 / 环形图 / 玫瑰图
│   ├── scatter.md              # 散点图 / 气泡图 / 涟漪图
│   ├── candlestick.md          # K线图 + 成交量 + 技术指标
│   ├── boxplot.md              # 箱形图统计分析
│   ├── heatmap.md              # 直角坐标 + 日历热力图
│   ├── radar.md                # 雷达图 / 蜘蛛图
│   ├── map.md                  # 区域着色 + 地理坐标 + 飞线
│   ├── tree.md                 # 可折叠树图 / 组织架构
│   ├── treemap.md              # 矩形树图（层级面积）
│   ├── sunburst.md             # 旭日图（多层级钻取）
│   ├── graph.md                # 力导向 / 环形关系图
│   ├── sankey.md               # 桑基图（流向图）
│   ├── parallel.md             # 平行坐标系
│   ├── chord.md                # 弦图（v6+）
│   ├── funnel.md               # 漏斗图
│   ├── gauge.md                # 仪表盘 / 进度环
│   ├── pictorialbar.md         # 象形柱图
│   ├── themeriver-calendar.md  # 主题河流图 + 日历图
│   ├── custom.md               # 自定义系列（renderItem）
│   ├── dataset-datazoom.md     # 数据集变换 + 数据缩放
│   ├── mixed-realtime.md       # 混合图表 + 实时更新
│   └── 3d-gl.md               # 3D 图表（echarts-gl）
│
└── references/
    ├── chart-types.md          # 所有系列类型及关键配置项
    └── options-reference.md   # 所有组件参考（tooltip、legend、dataZoom 等）
```

---

## ⚙️ 技能工作原理

本技能遵循 [GitHub Copilot 自定义指令](https://code.visualstudio.com/docs/copilot/copilot-customization) 格式。  
被引用时，Copilot 会加载 `SKILL.md`，获取关于 ECharts API 的结构化知识。

### 调用方式

当你的提示词涉及 ECharts 图表时，技能会自动触发。`SKILL.md` 中的 `description` 字段驱动语义匹配：

```yaml
description: "Create, configure, and customize Apache ECharts charts..."
argument-hint: "Describe the chart you want (e.g., 'bar chart comparing monthly sales')"
```

### 生成示例

Copilot 将生成完整、自包含的 `option` 配置对象：

```js
// 示例：「创建一个双 Y 轴图表，同时展示降雨量和气温」
const option = {
  tooltip: { trigger: 'axis', axisPointer: { type: 'cross' } },
  legend: { data: ['降雨量', '气温'] },
  xAxis: [{ type: 'category', data: ['1月','2月','3月','4月','5月','6月','7月','8月','9月','10月','11月','12月'] }],
  yAxis: [
    { type: 'value', name: '降雨量', axisLabel: { formatter: '{value} ml' } },
    { type: 'value', name: '气温', position: 'right', axisLabel: { formatter: '{value} °C' } }
  ],
  series: [
    { name: '降雨量', type: 'bar', data: [2.6, 5.9, 9.0, 26.4, 28.7, 70.7, 175.6, 182.2, 48.7, 18.8, 6.0, 2.3] },
    { name: '气温', type: 'line', yAxisIndex: 1, data: [2.0, 2.2, 3.3, 4.5, 6.3, 10.2, 20.3, 23.4, 23.0, 16.5, 12.0, 6.2] }
  ]
};
```

---

## 🔑 核心概念

### Option 配置对象

每个 ECharts 图表都由一个声明式的配置对象驱动：

| 顶层键 | 用途 |
|--------|------|
| `title` | 图表标题与副标题 |
| `legend` | 系列显示/隐藏切换 |
| `grid` | 直角坐标系布局（边距） |
| `xAxis` / `yAxis` | 直角坐标系轴配置 |
| `polar` / `radiusAxis` / `angleAxis` | 极坐标系轴 |
| `radar` | 雷达图指示器配置 |
| `geo` | 地理坐标背景层 |
| `tooltip` | 鼠标悬停提示框行为 |
| `toolbox` | 内置工具栏（保存图片、数据视图、缩放） |
| `dataZoom` | 滚动/滑动缩放组件 |
| `visualMap` | 数据 → 颜色/大小 映射 |
| `series` | **数组**，每项是一个系列，包含 `type`、`data`、`name` |
| `dataset` | 共享数据源（代替 `series.data` 中内联数据） |
| `color` | 全局调色板数组 |
| `backgroundColor` | 画布背景色 |
| `animation` | 是否开启动画 |

### 常用 API 方法

```js
const chart = echarts.init(dom, theme?, opts?);
chart.setOption(option, notMerge?, lazyUpdate?);
chart.resize({ width?, height? });
chart.on('click', params => { /* 事件处理 */ });
chart.off('click', handler);
chart.dispatchAction({ type: 'highlight', seriesIndex: 0, dataIndex: 2 });
chart.getDataURL({ type: 'png', pixelRatio: 2 });
chart.dispose();
echarts.registerTheme('myTheme', themeObj);   // 注册主题
echarts.registerMap('china', geoJSON);         // 注册地图
echarts.connect([chart1, chart2]);             // 联动多个图表
```

### 大数据量性能优化

```js
series: [{
  type: 'line',
  data: bigArray,          // 万级数据点
  sampling: 'lttb',        // 最大三角形三桶采样算法（降采样）
  large: true,             // 散点图：启用 GPU 加速大数据模式
  largeThreshold: 2000,    // 超过此数量时启用 large 模式
  progressive: 200,        // 每帧渲染 200 个数据点（渐进式）
  animation: false         // 大数据场景建议关闭动画
}]
```

---

## 📚 参考资源

| 资源 | 说明 |
|------|------|
| [examples.html](./examples.html) | **在线图表库** — 30 个实时渲染图表，含代码切换（浏览器打开） |
| [SKILL.md](./SKILL.md) | 技能主定义文件（Copilot 加载入口） |
| [examples/README.md](./examples/README.md) | 25 个示例文件索引（每种图表 2-3 个 option） |
| [assets/templates.md](./assets/templates.md) | React、Vue、tree-shaking 集成模板 |
| [assets/official-examples.md](./assets/official-examples.md) | 官方示例分类目录（含编辑器链接） |
| [references/chart-types.md](./references/chart-types.md) | 所有系列类型及关键配置项说明 |
| [references/options-reference.md](./references/options-reference.md) | 所有组件参考（tooltip、legend、dataZoom 等） |
| [官方文档](https://echarts.apache.org/zh/option.html) | ECharts 完整 option 配置文档（中文） |
| [官方 API](https://echarts.apache.org/zh/api.html) | ECharts 实例 API 参考（中文） |
| [示例库](https://echarts.apache.org/examples/zh/index.html) | 400+ 官方交互式示例（中文） |
