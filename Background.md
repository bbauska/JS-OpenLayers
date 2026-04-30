<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ Background.md ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h1>Background</h1>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Overview</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>OpenLayers is a modular, high-performance, feature-packed library for displaying and interacting 
with maps and geospatial data.</p>

<p>The library comes with built-in support for a wide range of commercial and free image and vector 
tile sources, and the most popular open and proprietary vector data formats. With OpenLayers's map 
projection support, data can be in any projection.</p>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Public API</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>OpenLayers is available as <a href="https://npmjs.com/package/ol">
ol npm package</a>, which provides all modules of the officially supported 
<a href="https://openlayers.org/apidoc">API</a>.</p>

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Browser Support</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>OpenLayers runs on all modern browsers (with greater than 1% global usage). This includes Chrome, 
Firefox, Safari and Edge. For older browsers, polyfills (<a href="https://polyfill-fastly.io/">
Fastly</a> or <a href="https://cdnjs.cloudflare.com/polyfill">Cloudflare</a>) will likely need to 
be added.</p>

<p>The library is intended for use on both desktop/laptop and mobile devices, and supports pointer 
and touch interactions.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Module and Naming Conventions</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>OpenLayers modules with CamelCase names provide classes as default exports, and may contain additional constants or functions as named exports:</p>

```
import Map from 'ol/Map.js';
import View from 'ol/View.js';
```

<p>Class hierarchies grouped by their parent are provided in a subfolder of the package, e.g. <mark>layer/</mark>.</p>

<p>For convenience, these are also available as named exports, e.g.</p>

```
import {Map, View} from 'ol';
import {Tile, Vector} from 'ol/layer.js';
```

<p>In addition to these re-exported classes, modules with lowercase names also provide constants or functions as named exports:</p>

```
import {getUid} from 'ol';
import {fromLonLat} from 'ol/proj.js';
```
