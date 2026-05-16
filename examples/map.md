# GEO / Map Chart Examples

> Official examples: https://echarts.apache.org/examples/en/index.html#chart-type-map
> 
> **Note**: Map charts require registering GeoJSON. Use `echarts.registerMap('name', geoJsonObj)`.  
> GeoJSON sources: https://github.com/apache/echarts/tree/master/test/data

---

## Example 1 — World Choropleth Map

**Use case**: Color countries by a quantitative metric (e.g., population, GDP).  
**Editor**: [map-world](https://echarts.apache.org/examples/en/editor.html?c=map-world)

```js
// Step 1: Fetch and register GeoJSON
fetch('https://cdn.jsdelivr.net/npm/world-atlas@2/countries-110m.json')
  .then(r => r.json())
  .then(world => {
    // Convert TopoJSON → GeoJSON or use a pre-converted file
    echarts.registerMap('world', { geoJSON: world });
    renderMap();
  });

function renderMap() {
  const chart = echarts.init(document.getElementById('chart'));
  const option = {
    title: { text: 'World Population 2023 (millions)', left: 'center' },
    tooltip: {
      trigger: 'item',
      formatter: p => p.name && p.value ? `${p.name}: ${p.value}M` : p.name
    },
    visualMap: {
      min: 0,
      max: 1500,
      left: 'left',
      top: 'bottom',
      text: ['High', 'Low'],
      calculable: true,
      inRange: { color: ['#e0f3f8', '#abd9e9', '#74add1', '#4575b4', '#313695'] }
    },
    series: [
      {
        name: 'Population',
        type: 'map',
        map: 'world',
        roam: true,
        emphasis: {
          label: { show: true },
          itemStyle: { areaColor: '#f5a623' }
        },
        data: [
          { name: 'China',          value: 1412 },
          { name: 'India',          value: 1380 },
          { name: 'United States',  value: 331 },
          { name: 'Indonesia',      value: 273 },
          { name: 'Pakistan',       value: 220 },
          { name: 'Brazil',         value: 215 },
          { name: 'Nigeria',        value: 206 },
          { name: 'Bangladesh',     value: 165 },
          { name: 'Russia',         value: 146 },
          { name: 'Mexico',         value: 130 }
        ]
      }
    ]
  };
  chart.setOption(option);
}
```

---

## Example 2 — Scatter on Map (City Markers)

**Use case**: Plot point data (earthquakes, offices, events) on a geographic base map.  
**Editor**: [geo-choropleth-scatter](https://echarts.apache.org/examples/en/editor.html?c=geo-choropleth-scatter)

```js
// Assumes world GeoJSON is already registered as 'world'
const offices = [
  { name: 'New York',    coord: [-74.0059, 40.7128], employees: 450 },
  { name: 'London',      coord: [-0.1278,  51.5074], employees: 380 },
  { name: 'Tokyo',       coord: [139.6917, 35.6895], employees: 320 },
  { name: 'Shanghai',    coord: [121.4737, 31.2304], employees: 290 },
  { name: 'Sydney',      coord: [151.2093,-33.8688], employees: 180 },
  { name: 'São Paulo',   coord: [-46.6333,-23.5505], employees: 140 },
  { name: 'Dubai',       coord: [55.2708,  25.2048], employees: 120 },
  { name: 'Singapore',   coord: [103.8198,  1.3521], employees: 200 }
];

const option = {
  title: { text: 'Global Office Locations', left: 'center' },
  tooltip: {
    trigger: 'item',
    formatter: p => `${p.name}<br/>Employees: ${p.value[2]}`
  },
  geo: {
    map: 'world',
    roam: true,
    itemStyle: {
      areaColor: '#e0e0e0',
      borderColor: '#999',
      borderWidth: 0.5
    },
    emphasis: {
      itemStyle: { areaColor: '#b8d4f5' }
    },
    zoom: 1.2
  },
  series: [
    {
      type: 'scatter',
      coordinateSystem: 'geo',
      data: offices.map(o => ({
        name: o.name,
        value: [...o.coord, o.employees]
      })),
      symbolSize: d => Math.sqrt(d[2]) * 1.5,
      label: {
        show: true,
        formatter: '{b}',
        position: 'right',
        fontSize: 11
      },
      itemStyle: {
        color: '#5470c6',
        opacity: 0.8
      },
      emphasis: {
        itemStyle: { color: '#ee6666' },
        label: { show: true, fontWeight: 'bold' }
      }
    }
  ]
};
```

---

## Example 3 — Flight Routes (Lines on Geo)

**Use case**: Show connections/flows between geographic locations with animated arcs.  
**Editor**: [lines-flight](https://echarts.apache.org/examples/en/editor.html?c=lines-flight)

```js
// Assumes world GeoJSON registered as 'world'
const routes = [
  { from: 'New York',  fromCoord: [-74.0059, 40.7128], to: 'London',    toCoord: [-0.1278, 51.5074] },
  { from: 'New York',  fromCoord: [-74.0059, 40.7128], to: 'Tokyo',     toCoord: [139.6917, 35.6895] },
  { from: 'London',    fromCoord: [-0.1278, 51.5074],  to: 'Dubai',     toCoord: [55.2708, 25.2048] },
  { from: 'London',    fromCoord: [-0.1278, 51.5074],  to: 'Singapore', toCoord: [103.8198, 1.3521] },
  { from: 'Singapore', fromCoord: [103.8198, 1.3521],  to: 'Sydney',    toCoord: [151.2093, -33.8688] },
  { from: 'Shanghai',  fromCoord: [121.4737, 31.2304], to: 'Los Angeles', toCoord: [-118.2437, 34.0522] }
];

const option = {
  title: { text: 'Global Flight Routes', left: 'center' },
  tooltip: { trigger: 'item' },
  geo: {
    map: 'world',
    roam: false,
    silent: true,
    itemStyle: { areaColor: '#1a1a2e', borderColor: '#16213e' },
    zoom: 1.1
  },
  series: [
    {
      type: 'lines',
      coordinateSystem: 'geo',
      data: routes.map(r => ({
        fromName: r.from,
        toName: r.to,
        coords: [r.fromCoord, r.toCoord]
      })),
      lineStyle: {
        color: '#a6c84c',
        width: 1,
        opacity: 0.4,
        curveness: 0.2
      },
      effect: {
        show: true,
        period: 6,
        trailLength: 0.7,
        color: '#fff',
        symbolSize: 4
      }
    },
    {
      // Hub cities
      type: 'effectScatter',
      coordinateSystem: 'geo',
      data: [
        { name: 'New York',    value: [-74.0059, 40.7128, 100] },
        { name: 'London',      value: [-0.1278, 51.5074, 90] },
        { name: 'Tokyo',       value: [139.6917, 35.6895, 85] },
        { name: 'Singapore',   value: [103.8198, 1.3521, 75] },
        { name: 'Dubai',       value: [55.2708, 25.2048, 60] },
        { name: 'Shanghai',    value: [121.4737, 31.2304, 70] },
        { name: 'Sydney',      value: [151.2093, -33.8688, 50] },
        { name: 'Los Angeles', value: [-118.2437, 34.0522, 65] }
      ],
      symbolSize: d => Math.sqrt(d.value[2]) * 0.8,
      rippleEffect: { brushType: 'stroke' },
      itemStyle: { color: '#a6c84c' },
      label: { show: true, formatter: '{b}', position: 'right', color: '#fff', fontSize: 10 }
    }
  ]
};
```
