<template>
  <div id="app">
    <div id="map"></div>
  </div>
</template>

<script>
import {applyStyle} from 'ol-mapbox-style';
import VectorTileLayer from 'ol/layer/VectorTile.js'
import 'ol/ol.css';
import Map from 'ol/Map';
import OSM from 'ol/source/OSM';
import TileLayer from 'ol/layer/Tile';
import View from 'ol/View';

export default {
  name: 'App',
  mounted() {
    const map = new Map({
      layers: [
        new TileLayer({
          source: new OSM(),
        }),
      ],
      target: 'map',
      view: new View({
        center: [0, 0],
        zoom: 2,
      }),
    });

    const layer = new VectorTileLayer({declutter: true});
    applyStyle(layer, process.env.VUE_APP_LAYER_URL, {accessToken: process.env.VUE_APP_MAPBOX_TOKEN});

    map.addLayer(layer)
  },
}
</script>

<style>
* {
  box-shadow: border-box;
}
body {
  margin: 0;
}
#map {
  width: 100vw;
  height: 100vh;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
