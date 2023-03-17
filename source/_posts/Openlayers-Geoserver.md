---
title: Openlayers - Geoserver
date: 2023-03-17 13:24:41
tags:
---

## Openlayer là gì

## Getting started

Tải file thư viện openlayers: https://github.com/openlayers/openlayers/releases/download/v6.8.0/v6.8.0-dist.zip

Index.html:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Openlayers tutorial</title>
    <link rel="stylesheet" href="./resources/ol/ol.css" />
    <link rel="stylesheet" href="./main.css" />
  </head>
  <body>
    <div id="map"></div>

    <!-- Script -->
    <script src="./resources/ol/ol.js"></script>
    <script src="main.js"></script>
  </body>
</html>
```

Main.css:

```css
#map {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
```

### Define map:

```js
var mapView = new ol.View({
  center: ol.proj.fromLonLat([72.585717, 23.021245]),
  zoom: 8,
});

var map = new ol.Map({
  target: "map",
  view: mapView,
});
```

### Tạo bản đồ nền:

```js
var osmTile = new ol.layer.Tile({
  title: "Open Street Map",
  visible: true,
  source: new ol.source.OSM(),
});
map.addLayer(osmTile);
```

### Thêm 1 layer từ geoserver API:

```js
var TruongHocTile = new ol.layer.Tile({
  title: "India States",
  source: new ol.source.TileWMS({
    url: "http://gconnect.hopto.org:8888/geoserver/BDS/wms",
    params: { LAYERS: "BDS:gis_osm_pois_free_1", TILED: true },
    serverType: "geoserver",
    visible: true,
  }),
});

map.addLayer(TruongHocTile);
```

Thay BDS:gis_osm_pois_free_1 trong Param thành tên layer muốn hiển thị

![](/images/OlPost/Screenshot_1.png)

Và đây là kết quả:
![](/images/OlPost/Screenshot_2.png)

### Add layer switcher

#### Dùng thư viện có sẵn

Tải 2 file js, css của lib:

JS: https://unpkg.com/ol-layerswitcher@4.1.1
Css: ttps://unpkg.com/ol-layerswitcher@4.1.1/dist/ol-layerswitcher.css

Import 2 file vào index.html

Add layerswitcher control:

```js
var layerSwitcher = new ol.control.LayerSwitcher({
  activationMode: "click",
  startActive: false,
  groupSelectStyle: "children",
});

map.addControl(layerSwitcher);
```

Và đây là kết quả:
![](/images/OlPost/Screenshot_3.png)

#### Tự tạo layerswitcher bằng logic

HTML:

```html
<h3>Layers</h3>
<input
  type="checkbox"
  id="osm"
  name="osm"
  value="Open Street Map"
  checked
  onchange="toggleLayer(event)"
/>
<label for="osm">Open Street Map</label>
<br />

<input
  type="checkbox"
  id="osmpf1"
  name="osmpf1"
  value="OSM Pois Free 1"
  checked
  onchange="toggleLayer(event)"
/>
<label for="osmpf1">OSM Pois Free 1</label>
<br />

<input
  type="checkbox"
  id="hr"
  name="hr"
  value="Huyen Region"
  checked
  onchange="toggleLayer(event)"
/>
<label for="hr">Huyen Region</label>
<br />
```

JS: Duyệt - tìm kiếm layer có title bằng với event.target.value

```js
function toggleLayer(e){
    var layerName = e.target.value;
    var isChecked = e.target.checked;
    var layerList = map.getLayers();

    layerList.forEach((e) => {
        if(layerName == e.get('title')){
            e.setVisible(isChecked)
        }
    })

}
```

Và đây là kết quả:
![](/images/OlPost/Screenshot_4.png)


### Add Mouse Position Control

```js
var mousePosition = new ol.control.MousePosition({
    projection: 'EPSG:4326',
    coordinateFormat: function(coordinate){
        return ol.coordinate.format(coordinate, '{y} {x}', 6);
    }
})

map.addControl(mousePosition)
```

![](/images/OlPost/Screenshot_5.png)


Note: Có thể thêm thuộc tính className vào v à css lại control

```js
var mousePosition = new ol.control.MousePosition({
    className: 'mousePosition'
    projection: 'EPSG:4326',
    coordinateFormat: function(coordinate){
        return ol.coordinate.format(coordinate, '{y} {x}', 6);
    }
})

map.addControl(mousePosition)
```

### Add ScaleLine control

```js
var scaleLine = new ol.control.ScaleLine({
    bar: true,
    text: true
})
map.addControl(scaleLine)
```
![](/images/OlPost/Screenshot_6.png)