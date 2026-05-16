# ECharts Code Templates

> **Chart type examples** are now in [`../examples/`](../examples/README.md) — 2-3 complete working `option` objects per chart type.  
> This file retains **framework integration patterns** (React, Vue, tree-shaking) that are unique to this template.

→ **[Browse all chart-type examples →](../examples/README.md)**  
→ **[Mixed/Real-Time chart patterns →](../examples/mixed-realtime.md)**  
→ **[Live visual gallery →](../examples.html)**

---

## React Integration

```jsx
import { useEffect, useRef } from 'react';
import * as echarts from 'echarts/core';
import { BarChart } from 'echarts/charts';
import { GridComponent, TooltipComponent, LegendComponent } from 'echarts/components';
import { CanvasRenderer } from 'echarts/renderers';

echarts.use([BarChart, GridComponent, TooltipComponent, LegendComponent, CanvasRenderer]);

export function EChartsComponent({ option, style }) {
  const ref = useRef(null);
  const chartRef = useRef(null);

  useEffect(() => {
    chartRef.current = echarts.init(ref.current);
    const observer = new ResizeObserver(() => chartRef.current?.resize());
    observer.observe(ref.current);
    return () => {
      observer.disconnect();
      chartRef.current?.dispose();
    };
  }, []);

  useEffect(() => {
    chartRef.current?.setOption(option, true);
  }, [option]);

  return <div ref={ref} style={{ width: '100%', height: 400, ...style }} />;
}
```

---

## Vue 3 Integration

```vue
<template>
  <div ref="chartEl" :style="{ width: '100%', height: height + 'px' }" />
</template>

<script setup>
import { ref, watch, onMounted, onUnmounted } from 'vue';
import * as echarts from 'echarts/core';
import { BarChart } from 'echarts/charts';
import { GridComponent, TooltipComponent } from 'echarts/components';
import { CanvasRenderer } from 'echarts/renderers';

echarts.use([BarChart, GridComponent, TooltipComponent, CanvasRenderer]);

const props = defineProps({
  option: { type: Object, required: true },
  height: { type: Number, default: 400 }
});

const chartEl = ref(null);
let chart = null;

onMounted(() => {
  chart = echarts.init(chartEl.value);
  chart.setOption(props.option);
  window.addEventListener('resize', () => chart.resize());
});

watch(() => props.option, (newOpt) => {
  chart?.setOption(newOpt, true);
}, { deep: true });

onUnmounted(() => {
  chart?.dispose();
  window.removeEventListener('resize', () => chart?.resize());
});
</script>
```

---

## Tree-Shakeable Import (Webpack / Vite)

```js
import * as echarts from 'echarts/core';

// Only import the charts and components you use
import { BarChart, LineChart, PieChart } from 'echarts/charts';
import {
  TitleComponent, TooltipComponent, LegendComponent,
  GridComponent, DataZoomComponent, VisualMapComponent
} from 'echarts/components';
import { CanvasRenderer } from 'echarts/renderers';

echarts.use([
  BarChart, LineChart, PieChart,
  TitleComponent, TooltipComponent, LegendComponent,
  GridComponent, DataZoomComponent, VisualMapComponent,
  CanvasRenderer
]);

export default echarts;
```
