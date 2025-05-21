# 来源
Fork from [cesium-heatmap-es6](https://github.com/cesium-plugin/)
> 由于上面的包运行存在bug并且许久没有维护了，故自己fork了一份，并进行了一些修改。
主要是对初始化半径中读取this.heatmapOptions错误调整成 \_options


## 安装
`npm install cqdlzx-cesium-heatmap`

## 文档

## 示例
```javascript
import { CesiumHeatmap, HeatmapPoint } from "cqdlzx-cesium-heatmap"

const defaultDataValue = [10, 500]
const defaultOpacityValue = [0, 1]
const points: HeatmapPoint[] = [];

fetch("/test.geojson", {
  method: "GET",
  headers: {
    "Content-Type": "application/json",
  },
}).then((response) => {
  response.json().then((data) => {
    if (data)
      data.features.forEach(function (feature) {
        const lon = feature.geometry.coordinates[0];
        const lat = feature.geometry.coordinates[1];
        points.push({
          x: lon - 0.05,
          y: lat - 0.04,
          value: 100 * Math.random(),
        });
      });
    cesiumHeatmap = new CesiumHeatmap(viewer, {
      zoomToLayer: true,
      points,
      heatmapDataOptions: {
        max: defaultDataValue[1],
        min: defaultDataValue[0],
      },
      heatmapOptions: {
        maxOpacity: defaultOpacityValue[1],
        minOpacity: defaultOpacityValue[0],
      },
    });
  });
});
```