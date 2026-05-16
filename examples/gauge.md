# Gauge Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-gauge

---

## Example 1 — KPI Dashboard Gauge

**Use case**: Show a single key metric against a scale (speed, score, progress).  
**Editor**: [gauge-simple](https://echarts.apache.org/examples/en/editor.html?c=gauge-simple)

```js
const option = {
  title: { text: 'Server CPU Usage', left: 'center' },
  series: [
    {
      type: 'gauge',
      min: 0,
      max: 100,
      startAngle: 200,
      endAngle: -20,
      radius: '80%',
      splitNumber: 10,
      axisLine: {
        lineStyle: {
          width: 20,
          color: [
            [0.3, '#67e0e3'],
            [0.7, '#37a2da'],
            [1,   '#fd666d']
          ]
        }
      },
      pointer: { itemStyle: { color: 'auto' } },
      axisTick: { distance: -25, length: 8, lineStyle: { color: '#fff', width: 2 } },
      splitLine: { distance: -30, length: 20, lineStyle: { color: '#fff', width: 3 } },
      axisLabel: { color: 'inherit', distance: 35, fontSize: 12 },
      detail: {
        valueAnimation: true,
        formatter: '{value}%',
        color: 'inherit',
        fontSize: 32,
        fontWeight: 'bold',
        offsetCenter: [0, '60%']
      },
      title: {
        offsetCenter: [0, '-15%'],
        fontSize: 18,
        color: '#666'
      },
      data: [{ value: 72, name: 'CPU Load' }]
    }
  ]
};
```

---

## Example 2 — Progress Ring Gauge (Multi-KPI)

**Use case**: Show multiple progress rings in a single gauge for a dashboard panel.  
**Editor**: [gauge-progress](https://echarts.apache.org/examples/en/editor.html?c=gauge-progress)

```js
const option = {
  title: { text: 'System Performance', left: 'center' },
  tooltip: { formatter: '{a} <br/>{b} : {c}%' },
  series: [
    {
      type: 'gauge',
      startAngle: 90,
      endAngle: -270,
      pointer: { show: false },
      progress: {
        show: true,
        overlap: false,
        roundCap: true,
        clip: false,
        itemStyle: { borderWidth: 1, borderColor: '#464646' }
      },
      axisLine: { lineStyle: { width: 40 } },
      splitLine: { show: false, distance: 0, length: 10 },
      axisTick: { show: false },
      axisLabel: { show: false },
      data: [
        {
          value: 70,
          name: 'CPU',
          title: { offsetCenter: ['0%', '-50%'] },
          detail: { valueAnimation: true, offsetCenter: ['0%', '-32%'] }
        },
        {
          value: 85,
          name: 'Memory',
          title: { offsetCenter: ['0%', '0%'] },
          detail: { valueAnimation: true, offsetCenter: ['0%', '18%'] }
        },
        {
          value: 42,
          name: 'Disk I/O',
          title: { offsetCenter: ['0%', '50%'] },
          detail: { valueAnimation: true, offsetCenter: ['0%', '68%'] }
        }
      ],
      title: { fontSize: 14, color: '#666' },
      detail: {
        width: 50,
        height: 14,
        fontSize: 14,
        color: 'inherit',
        borderColor: 'inherit',
        borderRadius: 20,
        borderWidth: 1,
        formatter: '{value}%'
      }
    }
  ]
};
```

---

## Example 3 — Stage Gauge (Color Zones + Animated Value)

**Use case**: Show a value in different risk/performance zones with distinct colors.  
**Editor**: [gauge-stage](https://echarts.apache.org/examples/en/editor.html?c=gauge-stage)

```js
// Animated live gauge that updates every second
const chart = echarts.init(document.getElementById('chart'));

const option = {
  series: [
    {
      type: 'gauge',
      min: 0,
      max: 200,
      axisLine: {
        lineStyle: {
          width: 30,
          color: [
            [0.25, '#67e0e3'],  // green zone: 0-50
            [0.5,  '#37a2da'],  // blue zone: 50-100
            [0.75, '#fddd60'],  // yellow zone: 100-150
            [1,    '#fd666d']   // red zone: 150-200
          ]
        }
      },
      pointer: {
        itemStyle: { color: 'auto' }
      },
      axisTick: {
        length: 8,
        lineStyle: { color: 'auto', width: 2 }
      },
      splitLine: {
        length: 20,
        lineStyle: { color: 'auto', width: 3 }
      },
      axisLabel: {
        color: '#464646',
        distance: 25,
        fontSize: 12
      },
      title: { show: false },
      detail: {
        valueAnimation: true,
        fontSize: 28,
        fontWeight: 'bold',
        formatter: '{value} ms',
        color: 'auto',
        offsetCenter: [0, '70%']
      },
      data: [{ value: 50, name: 'Response Time' }]
    }
  ]
};

chart.setOption(option);

// Simulate live updates
setInterval(() => {
  chart.setOption({
    series: [{
      data: [{ value: Math.round(Math.random() * 180 + 10), name: 'Response Time' }]
    }]
  });
}, 2000);
```
