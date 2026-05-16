# Candlestick Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-candlestick

---

## Example 1 — Basic OHLC Candlestick with Volume

**Use case**: Standard stock price chart with up/down candles and a volume subplot.  
**Editor**: [candlestick-simple](https://echarts.apache.org/examples/en/editor.html?c=candlestick-simple)

```js
const dates  = ['2024-01', '2024-02', '2024-03', '2024-04', '2024-05', '2024-06'];
// [open, close, low, high]
const prices = [
  [90, 95, 85, 100],
  [95, 88, 82, 97],
  [88, 105, 85, 108],
  [105, 98, 92, 110],
  [98, 115, 95, 118],
  [115, 108, 103, 120]
];
const volumes = [12000, 9500, 15000, 11000, 18000, 14000];
const upColor   = '#ec0000';
const downColor = '#00da3c';

const option = {
  title: { text: 'ACME Corp — Monthly OHLC', left: 'center' },
  tooltip: {
    trigger: 'axis',
    axisPointer: { type: 'cross' },
    formatter: params => {
      const c = params[0];
      return `${c.axisValue}<br/>
        Open: ${c.data[0]}<br/>
        Close: ${c.data[1]}<br/>
        Low: ${c.data[2]}<br/>
        High: ${c.data[3]}`;
    }
  },
  legend: { top: 30, data: ['OHLC', 'MA5', 'Volume'] },
  grid: [
    { left: '10%', right: '8%', height: '55%' },
    { left: '10%', right: '8%', top: '75%', height: '16%' }
  ],
  xAxis: [
    { type: 'category', data: dates, gridIndex: 0, scale: true },
    { type: 'category', data: dates, gridIndex: 1, scale: true, axisLabel: { show: false } }
  ],
  yAxis: [
    { scale: true, gridIndex: 0, name: 'Price ($)' },
    { scale: true, gridIndex: 1, name: 'Volume', splitNumber: 2 }
  ],
  series: [
    {
      name: 'OHLC',
      type: 'candlestick',
      data: prices,
      itemStyle: {
        color: upColor,
        color0: downColor,
        borderColor: upColor,
        borderColor0: downColor
      }
    },
    {
      name: 'Volume',
      type: 'bar',
      xAxisIndex: 1,
      yAxisIndex: 1,
      data: volumes,
      itemStyle: {
        color: params => prices[params.dataIndex][1] >= prices[params.dataIndex][0] ? upColor : downColor
      }
    }
  ]
};
```

---

## Example 2 — Candlestick with Moving Averages & Bollinger Bands

**Use case**: Technical analysis with MA5, MA20, and Bollinger Bands overlay.  
**Editor**: [candlestick-sh](https://echarts.apache.org/examples/en/editor.html?c=candlestick-sh)

```js
// Simulated daily close prices for MA calculation
const closeData = [85, 88, 84, 90, 92, 95, 91, 93, 97, 100,
                   96, 98, 102, 99, 104, 108, 105, 110, 107, 112];
const dates = closeData.map((_, i) => {
  const d = new Date('2024-01-01');
  d.setDate(d.getDate() + i);
  return d.toISOString().slice(0, 10);
});
const ohlc = closeData.map((c, i) => {
  const o = i === 0 ? 80 : closeData[i - 1];
  return [o, c, Math.min(o, c) - Math.random() * 3, Math.max(o, c) + Math.random() * 3];
});

function movingAvg(data, period) {
  return data.map((_, i) =>
    i < period - 1 ? null : (data.slice(i - period + 1, i + 1).reduce((s, v) => s + v, 0) / period).toFixed(2)
  );
}

function bollingerBands(data, period = 20, k = 2) {
  return data.map((_, i) => {
    if (i < period - 1) return [null, null, null];
    const slice = data.slice(i - period + 1, i + 1);
    const mean = slice.reduce((s, v) => s + v, 0) / period;
    const std = Math.sqrt(slice.reduce((s, v) => s + Math.pow(v - mean, 2), 0) / period);
    return [(mean + k * std).toFixed(2), mean.toFixed(2), (mean - k * std).toFixed(2)];
  });
}

const ma5  = movingAvg(closeData, 5);
const ma10 = movingAvg(closeData, 10);
const bb   = bollingerBands(closeData, 10);

const option = {
  title: { text: 'Technical Analysis — MA & Bollinger Bands', left: 'center' },
  tooltip: { trigger: 'axis', axisPointer: { type: 'cross' } },
  legend: { top: 30, data: ['OHLC', 'MA5', 'MA10', 'BB Upper', 'BB Lower'] },
  grid: { left: '3%', right: '4%', bottom: '3%', containLabel: true },
  xAxis: { type: 'category', data: dates },
  yAxis: { scale: true },
  series: [
    {
      name: 'OHLC', type: 'candlestick', data: ohlc,
      itemStyle: { color: '#ec0000', color0: '#00da3c', borderColor: '#8A0000', borderColor0: '#008F28' }
    },
    { name: 'MA5',      type: 'line', data: ma5,                              lineStyle: { opacity: 0.8 }, symbol: 'none' },
    { name: 'MA10',     type: 'line', data: ma10,                             lineStyle: { opacity: 0.8, type: 'dashed' }, symbol: 'none' },
    { name: 'BB Upper', type: 'line', data: bb.map(b => b[0]),                lineStyle: { color: '#aaa', type: 'dotted' }, symbol: 'none', areaStyle: { color: 'rgba(200,200,200,0.1)' } },
    { name: 'BB Lower', type: 'line', data: bb.map(b => b[2]),                lineStyle: { color: '#aaa', type: 'dotted' }, symbol: 'none' }
  ]
};
```

---

## Example 3 — Candlestick with Brush Selection

**Use case**: Allow user to select a range for detailed inspection.  
**Editor**: [candlestick-brush](https://echarts.apache.org/examples/en/editor.html?c=candlestick-brush)

```js
const option = {
  title: { text: 'Interactive Candlestick with Brush', left: 'center' },
  tooltip: { trigger: 'axis', axisPointer: { type: 'cross' } },
  toolbox: {
    feature: {
      dataZoom: { yAxisIndex: 'none' },
      brush: { type: ['lineX', 'clear'] },
      restore: {},
      saveAsImage: {}
    }
  },
  brush: {
    xAxisIndex: 'all',
    brushLink: 'all',
    outOfBrush: { colorAlpha: 0.1 }
  },
  dataZoom: [
    { type: 'inside', xAxisIndex: [0], start: 50, end: 100 },
    { type: 'slider', xAxisIndex: [0], start: 50, end: 100 }
  ],
  xAxis: {
    type: 'category',
    data: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug']
  },
  yAxis: { scale: true },
  series: [
    {
      name: 'OHLC',
      type: 'candlestick',
      // [open, close, low, high]
      data: [
        [20, 34, 10, 38], [40, 35, 30, 50], [31, 38, 33, 44],
        [38, 15, 5,  42], [25, 28, 20, 35], [30, 40, 28, 45],
        [35, 30, 25, 38], [32, 42, 30, 48]
      ],
      itemStyle: { color: '#ec0000', color0: '#00da3c', borderColor: '#8A0000', borderColor0: '#008F28' }
    }
  ]
};
```
