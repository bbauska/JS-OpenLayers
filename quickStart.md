<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ quickStart.md ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h1>Quick Start</h1>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>This primer shows you how to put a map on a web page. The development setup uses 
<a href="https://nodejs.org/">Node</a> (14 or higher) and requires that you have 
<a href="https://github.com/git-guides/install-git">git</a> installed.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Set up a new project</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>The easiest way to start building a project with OpenLayers is to run <mark>npm create ol-app</mark>:</p>

```
npm create ol-app my-app
cd my-app
npm start
```

<p>The <b>first command</b> will create a directory called <mark>my-app</mark> (you can use a different 
name if you wish), install OpenLayers and a development server, and set up a basic app with 
<mark>index.html</mark>, <mark>main.js</mark>, and <mark>style.css</mark> files.</p>

<p>The <b>second command (<mark>cd my-app</mark>)</b> changes the working directory to your new 
<mark>my-app</mark> project so you can start working with it.</p>

<p>The <b>third command (<mark>npm start</mark>)</b> starts a development server so you can view 
your application in a browser while working on it. After running npm start, you'll see output that 
tells you the URL to open. Open <a href="http://localhost:5173/">http://localhost:5173/</a> (or 
whatever URL is displayed) to see your new application.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Exploring the parts</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>An OpenLayers application is composed of three basic parts:</p>

<p>The HTML markup with an element to contain the map (<mark>index.html</mark>)
The JavaScript that initializes the map (<mark>main.js</mark>)
The CSS styles that determine the map size and any other customizations (<mark>style.css</mark>)</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>The markup</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Open the <mark>index.html</mark> file in a text editor. It should look something like this:</p>

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Quick Start</title>
  </head>
  <body>
    <div id="map"></div>
    <script type="module" src="./main.js"></script>
  </body>
</html>
```

<p>The two important parts in the markup are the <mark>&lt;div&gt;</mark> element to contain the map 
and the <mark>&lt;script&gt;</mark> tag to pull in the JavaScript. The map container or target 
should be a block level element (like a <mark>&lt;div&gt;</mark>) and it must appear in the document 
before the <mark>&lt;script&gt;</mark> tag that initializes the map.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>The script</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Open the <mark>main.js</mark> file in a text editor. It should look something like this:</p>

```
import './style.css';
import Map from 'ol/Map.js';
import OSM from 'ol/source/OSM.js';
import TileLayer from 'ol/layer/Tile.js';
import View from 'ol/View.js';

const map = new Map({
  target: 'map',
  layers: [
    new TileLayer({
      source: new OSM(),
    }),
  ],
  view: new View({
    center: [0, 0],
    zoom: 2,
  }),
});
```

<p>OpenLayers is packaged as a collection of <a href="https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/">
ES modules</a>. The <mark>import</mark> lines are used to pull in the modules that your application 
needs. Take a look through the <a href="https://openlayers.org/en/latest/examples/">examples</a> and 
<a href="https://openlayers.org/en/latest/apidoc/">API docs</a> to understand which modules you might 
want to use.</p>

<p>The <mark>import './style.css';</mark> line might be a bit unexpected. In this example, 
we're using <a href="https://vitejs.dev/">Vite</a> as a development server. Vite allows CSS 
to be imported from JavaScript modules. If you were using a different development server, 
you might include the <mark>style.css</mark> in a <mark>&lt;link&gt;</mark> tag in the 
<mark>index.html</mark> instead.</p>

<p>The <mark>main.js</mark> module serves as an entry point for your application. It initializes a 
new map, giving it a single layer with an OSM source and a view describing the center and zoom level. 
Read through the <a href="https://openlayers.org/doc/tutorials/concepts.html">Basic Concepts 
tutorial</a> to learn more about <mark>Map</mark>, <mark>View</mark>, <mark>Layer</mark>, and 
<mark>Source</mark> components.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h3>The style</h3>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>Open the <mark>style.css</spna> file in a text editor. It should look something like this:</p>

```
@import "node_modules/ol/ol.css";

html,
body {
  margin: 0;
  height: 100%;
}

#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
```

<p>The first line imports the <mark>ol.css</mark> file that comes with the <mark>ol</mark> package 
(OpenLayers is published as the <a href="https://www.npmjs.com/package/ol">ol package</a> in the 
npm registry). The <mark>ol</mark> package was installed in the <mark>npm create ol-app</mark> 
step above. If you were starting with an existing application instead of using <mark>npm create 
ol-app</mark>, you would install the package with <mark>npm install ol</mark>. The <mark>ol.css</mark> 
stylesheet includes styles for the elements that OpenLayers creates – things like buttons for 
zooming in and out.</p>

<p>The remaining rules in the <mark>style.css</mark> file make it so the <mark>&lt;div id="map"&gt;</mark> 
element that contains the map fills the entire page.</p>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2>Deploying your app</h2>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<p>You can make edits to the <mark>index.html</mark>, <mark>main.js</mark>, or <mark>style.css</mark> 
files and see the resulting change in your browser while running the development server (with <mark>npm 
start</mark>). After you have finished making edits, it is time to bundle or build your application so 
that it can be deployed as a static website (without needing to run a development server like Vite).</p>

<p>To build your application, run the following:</p>

```
npm run build
```

<p>This will create a <mark>dist</mark> directory with a new <mark>index.html</mark> and assets that make up 
your application. These <mark>dist</mark> files can be deployed with your production website.</p>
