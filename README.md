# Leaflet.EdgeMarker

A reusable Leaflet plugin that displays directional arrows at the map edges when markers move outside the current viewport.

## Overview

Leaflet.EdgeMarker enhances map navigation by providing visual cues for off-screen map objects. When markers, circles, or other map objects move outside the visible area due to panning or zooming, this plugin displays arrow indicators at the map's edges that point toward these off-screen objects.

## Features

- Shows directional arrows at map edges for off-screen objects
- Arrows automatically rotate to point toward off-screen objects
- Supports filtering to show edge markers only for specific object types
- Compatible with all standard Leaflet markers and shapes
- Customizable appearance through CSS and options
- Lightweight and performance-optimized

## Installation

### Using npm

```bash
npm install leaflet-edge-marker
```

### Manual Installation

1. Download the `leaflet-edge-marker.js` file
2. Include it in your HTML after Leaflet:

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.css" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.min.js"></script>
<script src="path/to/leaflet-edge-marker.js"></script>
```

## Basic Usage

```javascript
// Create a Leaflet map
var map = L.map('map').setView([51.2, 10.43], 6);

// Add a tile layer
L.tileLayer('https://{s}.tile.osm.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
}).addTo(map);

// Add some markers to the map
L.marker([48.85, 2.35]).addTo(map);   // Paris
L.marker([52.52, 13.40]).addTo(map);  // Berlin

// Add EdgeMarker to the map with default options
var edgeMarkerLayer = L.edgeMarker().addTo(map);
```

## Configuration Options

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `icon` | L.Icon | Default arrow icon | The icon to use for edge markers |
| `rotateIcons` | Boolean | `true` | Whether to rotate icons based on the relative position of off-screen objects |
| `layerGroup` | L.LayerGroup | `null` | Optional layer group to use for edge markers |
| `className` | String | `'leaflet-edge-marker'` | CSS class name for styling edge markers |
| `objectFilter` | Function | `null` | Optional function to filter which objects get edge markers |

## Advanced Usage

### Custom Icon

```javascript
var edgeMarkerLayer = L.edgeMarker({
    icon: L.icon({
        iconUrl: 'path/to/custom-arrow.png',
        iconSize: [32, 32],
        iconAnchor: [16, 16]
    })
}).addTo(map);
```

### Filtering Objects

```javascript
// Only show edge markers for marker objects, not circles or polygons
var edgeMarkerLayer = L.edgeMarker({
    objectFilter: function(layer) {
        return layer instanceof L.Marker;
    }
}).addTo(map);
```

### Custom Styling

Add custom CSS to style the edge markers:

```css
.leaflet-edge-marker img {
    background-color: rgba(255, 255, 255, 0.7);
    border-radius: 50%;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
}
```

## Methods

| Method | Returns | Description |
|--------|---------|-------------|
| `addTo(map)` | `this` | Adds the EdgeMarker to the specified map |
| `addLayer(layer)` | `this` | Manually adds a layer to be tracked by EdgeMarker |
| `removeLayer(layer)` | `this` | Manually removes a layer from being tracked |
| `update()` | `this` | Forces an update of all edge markers |
| `destroy()` | - | Removes all edge markers and cleans up event listeners |

## Events

EdgeMarker doesn't emit any custom events, but it listens to the following map events:

- `move`: Updates edge markers when the map is panned
- `viewreset`: Updates edge markers when the map zoom changes
- `resize`: Updates edge markers when the map container is resized
- `layeradd`: Tracks new layers added to the map
- `layerremove`: Stops tracking layers removed from the map

## Browser Support

Leaflet.EdgeMarker works in all browsers that support Leaflet.

## License

MIT License

## Acknowledgements

Based on the original concept by [ubergesundheit](https://github.com/ubergesundheit/Leaflet.EdgeMarker).
