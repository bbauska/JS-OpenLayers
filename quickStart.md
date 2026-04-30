# Quick Start
This primer shows you how to put a map on a web page. The development setup uses <a href="https://nodejs.org/">
Node</a> (14 or higher) and requires that you have <a href="https://github.com/git-guides/install-git">git</a> installed.

## Set up a new project
The easiest way to start building a project with OpenLayers is to run <span>npm create ol-app</span>:

```
npm create ol-app my-app
cd my-app
npm start
```

The <b>first command</b> will create a directory called <span>my-app</span> (you can use a different 
name if you wish), install OpenLayers and a development server, and set up a basic app with 
<span>index.html</span>, <span>main.js</span>, and <span>style.css</span> files.

The <b>second command (<span>cd my-app</span>)</b> changes the working directory to your new <span>my-app</span> project so you can 
start working with it.

The <b>third command (<span>npm start</span>)</b> starts a development server so you can view your application in a browser 
while working on it. After running npm start, you'll see output that tells you the URL to open. Open 
<a href="http://localhost:5173/">http://localhost:5173/</a> (or whatever URL is displayed) to see your new application.

## Exploring the parts
An OpenLayers application is composed of three basic parts:

The HTML markup with an element to contain the map (<span>index.html</span>)
The JavaScript that initializes the map (<span>main.js</span>)
The CSS styles that determine the map size and any other customizations (<span>style.css</span>)

### The markup
Open the <span>index.html</span> file in a text editor. It should look something like this:

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

The two important parts in the markup are the <span>&lt;div&gt;</span> element to contain the map 
and the <span>&lt;script&gt;</span> tag to pull in the JavaScript. The map container or target 
should be a block level element (like a <span>&lt;div&gt;</span>) and it must appear in the document 
before the <span>&lt;script&gt;</span> tag that initializes the map.

### The script
Open the <span>main.js</span> file in a text editor. It should look something like this:

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

OpenLayers is packaged as a collection of <a href="https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/">>ES modules</a>. The <span>import</span> lines are used to pull in the modules that your application needs. Take a look through the <a href="https://openlayers.org/en/latest/examples/">examples</a> and <a href="https://openlayers.org/en/latest/apidoc/">API docs</a> to understand which modules you might want to use.

The <span>import './style.css';</span> line might be a bit unexpected. In this example, we're using <a href="https://vitejs.dev/">Vite</a> as a development server. Vite allows CSS to be imported from JavaScript modules. If you were using a different development server, you might include the <span>style.css</span> in a <span>&lt;link&gt;</span> tag in the <span>index.html</span> instead.

The <span>main.js</span> module serves as an entry point for your application. It initializes a new 
map, giving it a single layer with an OSM source and a view describing the center and zoom level. 
Read through the <a href="https://openlayers.org/doc/tutorials/concepts.html">Basic Concepts tutorial</a> 
to learn more about <span>Map</span>, <span>View</span>, <span>Layer</span>, and <span>Source</span> components.

### The style
Open the <span>style.css</spna> file in a text editor. It should look something like this:

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

The first line imports the <span>ol.css</span> file that comes with the <span>ol</span> package 
(OpenLayers is published as the <a href="https://www.npmjs.com/package/ol">ol package</a> in the 
npm registry). The <span>ol</span> package was installed in the <span>npm create ol-app</span> step above. If you were 
starting with an existing application instead of using <span>npm create ol-app</span>, you would install the 
package with <span>npm install ol</span>. The <span>ol.css</span> stylesheet includes styles for the elements that OpenLayers 
creates – things like buttons for zooming in and out.

The remaining rules in the <span>style.css</span> file make it so the <span>&lt;div id="map"&gt;</span> element that contains the map fills the entire page.

## Deploying your app
You can make edits to the <span>index.html</span>, <span>main.js</span>, or <span>style.css</span> 
files and see the resulting change in your browser while running the development server (with <span>npm 
start</span>). After you have finished making edits, it is time to bundle or build your application so 
that it can be deployed as a static website (without needing to run a development server like Vite).

To build your application, run the following:

```
npm run build
```

This will create a <span>dist</span> directory with a new <span>index.html</span> and assets that make up 
your application. These <span>dist</span> files can be deployed with your production website.

Code license
