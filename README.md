# Leaflet Measure Polygon Plugin Documentation

## Overview

The Leaflet Measure Polygon plugin allows users to measure the area and perimeter of polygons drawn on a Leaflet map. It is built on top of Leaflet.js and requires the following dependencies:

1. [Leaflet](https://unpkg.com/leaflet@1.7.1/dist/leaflet.js)
2. [Leaflet.draw](https://unpkg.com/leaflet-draw@1.0.4/dist/leaflet.draw.js)
3. [Leaflet.Editable](https://npmcdn.com/leaflet-editable@0.6.2/src/Leaflet.Editable.js)
4. [Leaflet-Measure-Path](https://prominentedge.com/leaflet-measure-path/leaflet-measure-path.js)

## Installation

To use the plugin, include the following files in your HTML file:

```html
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css" />
<link rel="stylesheet" href="https://unpkg.com/leaflet-draw@1.0.4/dist/leaflet.draw.css" />
<script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"></script>
<script src="https://unpkg.com/leaflet-draw@1.0.4/dist/leaflet.draw.js"></script>
<link rel="stylesheet" href="../leaflet-measure-path.css" />
<script src="auxiliares/editable.js"></script>
<script src="auxiliares/measure.js"></script>
```

Then, add the plugin code to your project. You can find the full code for the plugin in the original question.

## Usage

To add the Measure Polygon control to your map, first initialize your map with the `editable` option set to `true`. Then, create a new instance of the `L.Control.MeasurePolygon` control and add it to your map:

```javascript
const map = L.map('map', { editable: true }).setView([51.505, -0.09], 13);
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
}).addTo(map);

const measurePolygonControl = L.control.measurePolygon();
measurePolygonControl.addTo(map);
```

## Options

The plugin can be customized with various options:

| Option | Type | Default | Description |
| --- | --- | --- | --- |
| position | String | 'topright' | Position of the control on the map. |
| icon_active | String | URL | URL of the active state icon. |
| icon_inactive | String | URL | URL of the inactive state icon. |
| html_template | String | Template | HTML template for displaying the measurement results. |
| height | Number | 130 | Height of the measurement results panel. |
| width | Number | 150 | Width of the measurement results panel. |
| color_polygon | String | 'black' | Color of the polygon outline. |
| fillColor_polygon | String | 'yellow' | Fill color of the polygon. |
| weight_polygon | String | '2' | Width of the polygon outline. |
| checkonedrawpoligon | Boolean | false | Whether only one polygon can be drawn at a time. |
| msj_disable_tool | String | '¿Desea desabilitar la herramienta?' | Message displayed when disabling the tool. |

To customize the plugin with these options, pass an object with the desired options when creating a new instance of the `L.Control.MeasurePolygon` control:

```javascript
const customOptions = {
    icon_active: 'https://example.com/icon-active.png',
    icon_inactive: 'https://example.com/icon-inactive.png',
    color_polygon: 'blue',
    fillColor_polygon: 'green',
    weight_polygon: 3,
    checkonedrawpoligon: true,
    msj_disable_tool: 'Do you want to disable the tool?'
};

const measurePolygonControl = L.control.measurePolygon(customOptions);
measurePolygonControl.addTo(map);
```

## Internationalization

To make the plugin accessible to users of different languages, consider adding internationalization support. One approach to achieve this is to allow text labels, such as "Area" and "Perimeter," to be configurable through the plugin options. This way, you can provide custom translations when creating an instance of the control.

For example, add the following options to the `options` object in the `L.Control.MeasurePolygon` class definition:

```javascript
label_area: 'Area',
label_perimeter: 'Perimeter',
```

Then, update the `_UpdateAreaPerimetro` method to use these options instead of the static text labels:

```javascript
let areaValue = `${this.options.label_area}: ${area.toLocaleString('en-US', options)} m²`;
let perimeterValue = `${this.options.label_perimeter}: ${perimeter.toLocaleString('en-US',options)} m`;
```

Now, when creating an instance of the control, you can provide custom translations for the text labels:

```javascript
const customOptions = {
    label_area: 'Fläche',
    label_perimeter: 'Umfang'
};

const measurePolygonControl = L.control.measurePolygon(customOptions);
measurePolygonControl.addTo(map);
```

This approach will allow you to adapt the plugin to different languages according to the needs of your users.

## Mobile Device Compatibility

To ensure the plugin works correctly on mobile devices, verify that the layout and interaction are appropriate for touchscreens. For example, you could increase the size of the icons and controls to make them easier to use on mobile devices.

Also, make sure that the Leaflet libraries and related plugins are compatible with mobile devices. Leaflet itself is mobile-friendly, but some plugins may require additional adjustments to ensure an optimal user experience on touchscreens.

## Testing and Troubleshooting

As you customize and expand the plugin's functionality, it's essential to perform tests on different browsers and devices to ensure compatibility and performance. Make sure to test in the latest versions of major browsers, such as Chrome, Firefox, Safari, and Edge, as well as on mobile devices and tablets.

If you encounter issues or bugs, investigate whether these are related to the plugin itself, the Leaflet libraries, additional plugins, or your project's configuration. Use your browser's development tools to inspect elements, debug code, and analyze the plugin's performance. If necessary, consult Leaflet's documentation and related libraries for additional information on how to troubleshoot specific issues.
