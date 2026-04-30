<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ basicConcepts.md ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
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

<h2>View</h2>
The map is not responsible for things like center, zoom level and projection of the map. Instead, these 
are properties of a <mark>ol/View</mark> instance.

```
import View from 'ol/View.js';

map.setView(new View({
  center: [0, 0],
  zoom: 2,
}));
```

<p>A <mark>View</mark> also has a <mark>projection</mark>. The projection determines the coordinate system 
of the <mark>center</mark> and the units for map resolution calculations. If not specified (like in the 
above snippet), the default projection is Spherical Mercator (EPSG:3857), with meters as map units.</p>

<p>The <mark>zoom</mark> option is a convenient way to specify the map resolution. The available zoom 
levels are determined by <mark>maxZoom</mark> (default: 28), <mark>zoomFactor</mark> (default: 2) 
and <mark>maxResolution</mark> (default is calculated in such a way that the projection's validity 
extent fits in a 256x256 pixel tile). Starting at zoom level 0 with a resolution of <mark>maxResolution</mark> 
units per pixel, subsequent zoom levels are calculated by dividing the previous zoom level's resolution by 
<mark>zoomFactor</mark>, until zoom level <mark>maxZoom</mark> is reached.</p>

<h2>Source</h2>
<p>To get remote data for a layer, OpenLayers uses <mark>ol/source/Source</mark> subclasses. These are 
available for free and commercial map tile services like OpenStreetMap or Bing, for OGC sources like 
WMS or WMTS, and for vector data in formats like GeoJSON or KML.</p>

```
import OSM from 'ol/source/OSM.js';

const source = new OSM();
```

<h2>Layer</h2>
<p>A layer is a visual representation of data from a source. OpenLayers has four basic types of layers:</p>

  - <mark>ol/layer/Tile</mark> - Renders sources that provide tiled images in grids that are organized by zoom levels for specific resolutions.
  - <mark>ol/layer/Image</mark> - Renders sources that provide map images at arbitrary extents and resolutions.
  - <mark>ol/layer/Vector</mark> - Renders vector data client-side.
  - <mark>ol/layer/VectorTile</mark> - Renders data that is provided as vector tiles.

```
import TileLayer from 'ol/layer/Tile.js';

// ...
const layer = new TileLayer({source: source});
map.addLayer(layer);
```

<h2>Putting it all together</h2>
<p>The above snippets can be combined into a single script that renders a map with a single tile layer:</p>

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
