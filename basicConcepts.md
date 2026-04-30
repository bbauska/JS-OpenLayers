<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h1>Basic Concepts</h1>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Map</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>The core component of OpenLayers is the map (from the <mark>ol/Map</mark> module). It is 
rendered to a <mark>target</mark> container (e.g. a <mark>div</mark> element on the web page 
that contains the map). All map properties can either be configured at construction time, or 
by using setter methods, e.g. <mark>setTarget()</mark>.</p>

<p>The markup below could be used to create a <mark>&lt;div&gt;</mark> that contains your map.</p>

```
<div id="map" style="width: 100%; height: 400px"></div>
```

<p>The script below constructs a map that is rendered in the <mark>&lt;div&gt;</mark> above, using 
the <mark>map</mark> id of the element as a selector.</p>

```
import Map from 'ol/Map.js';

const map = new Map({target: 'map'});
```

View
The map is not responsible for things like center, zoom level and projection of the map. Instead, these are properties of a ol/View instance.

```
import View from 'ol/View.js';

map.setView(new View({
  center: [0, 0],
  zoom: 2,
}));
```

A View also has a projection. The projection determines the coordinate system of the center and the units for map resolution calculations. If not specified (like in the above snippet), the default projection is Spherical Mercator (EPSG:3857), with meters as map units.

The zoom option is a convenient way to specify the map resolution. The available zoom levels are determined by maxZoom (default: 28), zoomFactor (default: 2) and maxResolution (default is calculated in such a way that the projection's validity extent fits in a 256x256 pixel tile). Starting at zoom level 0 with a resolution of maxResolution units per pixel, subsequent zoom levels are calculated by dividing the previous zoom level's resolution by zoomFactor, until zoom level maxZoom is reached.

Source
To get remote data for a layer, OpenLayers uses ol/source/Source subclasses. These are available for free and commercial map tile services like OpenStreetMap or Bing, for OGC sources like WMS or WMTS, and for vector data in formats like GeoJSON or KML.

```
import OSM from 'ol/source/OSM.js';

const source = new OSM();
```

Layer
A layer is a visual representation of data from a source. OpenLayers has four basic types of layers:

  - ol/layer/Tile - Renders sources that provide tiled images in grids that are organized by zoom levels for specific resolutions.
  - ol/layer/Image - Renders sources that provide map images at arbitrary extents and resolutions.
  - ol/layer/Vector - Renders vector data client-side.
  - ol/layer/VectorTile - Renders data that is provided as vector tiles.

```
import TileLayer from 'ol/layer/Tile.js';

// ...
const layer = new TileLayer({source: source});
map.addLayer(layer);
```

Putting it all together
The above snippets can be combined into a single script that renders a map with a single tile layer:

```
import Map from 'ol/Map.js';
import View from 'ol/View.js';
import OSM from 'ol/source/OSM.js';
import TileLayer from 'ol/layer/Tile.js';

new Map({
  layers: [
    new TileLayer({source: new OSM()}),
  ],
  view: new View({
    center: [0, 0],
    zoom: 2,
  }),
  target: 'map',
});
```
