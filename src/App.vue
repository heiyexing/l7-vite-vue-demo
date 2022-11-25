<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import {
  PolygonLayer,
  GaodeMap,
  PointLayer,
  LineLayer,
  Scene,
  LayerPopup,
} from "@antv/l7";
import { featureCollection, point, circle } from "@turf/turf";

const newScene = new Scene({
  id: "map",
  map: new GaodeMap({
    style: "dark",
    center: [120.104697, 30.260704],
    pitch: 0,
    zoom: 15,
  }),
  // logoVisible: false,
});
newScene.on("loaded", () => {
  const pointLayer = new PointLayer({
    name: "pointLayer",
  });
  pointLayer
    .source(
      featureCollection([
        point([120.105697, 30.260704], {
          name: "测试点1",
          lng: 120.104697,
          lat: 30.260704,
        }),
        point([120.103697, 30.260704], {
          name: "测试点1",
          lng: 120.104697,
          lat: 30.260704,
        }),
      ])
    )
    .color("#ffffff")
    .shape("circle")
    .size(10);

  const polygonLayer = new PolygonLayer({
    name: "polygonLayer",
  });
  polygonLayer
    .source(
      featureCollection([
        circle([120.104697, 30.260704], 30, {
          units: "meters",
          properties: {
            name: "测试点1",
            lng: 120.104697,
            lat: 30.260704,
          },
        }),
        circle([120.104697, 30.261715], 30, {
          units: "meters",
          properties: {
            name: "测试点1",
            lng: 120.104697,
            lat: 30.260704,
          },
        }),
      ])
    )
    .color("#ff0000")
    .shape("fill");

  const lineString = new LineLayer({
    name: "lineLayer",
  });
  lineString
    .source(
      featureCollection([
        {
          type: "Feature",
          properties: {
            name: "测试线3",
          },
          geometry: {
            type: "LineString",
            coordinates: [
              [120.103615, 30.262026],
              [120.103172, 30.261771],
              [120.102697, 30.261934],
            ],
          },
        },
      ])
    )
    .size(6)
    .color("#00ff00");
  newScene.addLayer(pointLayer);
  newScene.addLayer(polygonLayer);
  newScene.addLayer(lineString);
  // pointLayer.on('mousemove', (e) => {
  //   console.log('point mousemove', e);
  // });
  // polygonLayer.on('mousemove', (e) => {
  //   console.log('polygon mousemove', e);
  // });
  // lineString.on('mousemove', (e) => {
  //   console.log('line mousemove', e);
  // });
});
</script>

<template>
  <div id="map" style="width: 100vw; height: 100vh; position: relative"></div>
</template>

<style scoped></style>
