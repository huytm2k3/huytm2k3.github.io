---
title: Openlayers
date: 2023-03-17 08:52:42
tags:
---

## Openlayers là gì

OpenLayers là một thư viện JavaScript mã nguồn mở để hiển thị dữ liệu bản đồ trong trình duyệt web dưới dạng bản đồ trơn. Nó cung cấp một API để xây dựng các ứng dụng địa lý dựa trên web phong phú tương tự như Google Maps và Bing Maps. 

Nguồn: Google

## Getting started

Cấu trúc openlayers cơ bản - cdn:

```html
<!doctype html>
<html lang="en">
  <head>
    <link rel="stylesheet" href="https://cdn.rawgit.com/openlayers/openlayers.github.io/master/en/v6.4.3/css/ol.css" type="text/css">
    <style>
      .map {
        height: 800px;
        width: 100%;
      }
    </style>
    <script src="https://cdn.rawgit.com/openlayers/openlayers.github.io/master/en/v6.4.3/build/ol.js"></script>
    <title>OpenLayers example</title>
  </head>
  <body>
    <h2>My Map</h2>
    <div id="map" class="map"></div>
    <script type="text/javascript">
      var map = new ol.Map({
        target: 'map',
        layers: [
        <!-- base map -->
          new ol.layer.Tile({
            source: new ol.source.OSM()
          })
        ],
        <!-- Vị trí camera khi vừa khởi động -->
        view: new ol.View({
          center: ol.proj.fromLonLat([37.41, 8.82]),
          zoom: 4
        })
      });
    </script>
  </body>
</html>
```