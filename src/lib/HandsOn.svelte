<script lang="ts">
  import Map from "ol/Map";
  import View from "ol/View";
  import TileLayer from "ol/layer/Tile";
  import VectorLayer from "ol/layer/Vector";
  import { useGeographic } from "ol/proj";
  import { OSM, Vector } from "ol/source";
  import Stamen from "ol/source/Stamen";
  import { Feature } from "ol";
  import { Style, Icon } from "ol/style";
  import { Point, MultiPoint } from "ol/geom";
  import XYZ from "ol/source/XYZ";
  let mapId = "20";
  // Local state
  let map: Map = null;

  useGeographic();

  const setupMap = (node) => {
    const osmLayer = new TileLayer({
      source: new Stamen({ layer: "toner-lite" }),
    });
    map = new Map({
      target: node.id,
      layers: [
        osmLayer,
        new VectorLayer({
          source: new Vector({
            features: [
              new Feature({
                geometry: new MultiPoint([
                  [37.5286, 55.7039],
                  [37.5386, 55.7139],
                ]),
              }),
            ],
          }),
          style: new Style({
            image: new Icon({
              anchor: [0.5, 1],
              src: "./warehouse.png",
              scale: 1,
            }),
          }),
        }),
      ],
      controls: [],
      view: new View({
        center: [33, 57],
        extent: [37.0286, 55.4039, 38.0286, 56.039],
        zoom: 8,
      }),
    });
    return {
      destroy() {
        if (map) {
          // as Map
          map.setTarget(null);
          map = null;
        }
      },
    };
  };
  const addLayer = () => {
    map &&
      map.getLayers().setAt(
        2,
        new VectorLayer({
          source: new Vector({
            features: [
              new Feature({ geometry: new Point([37.5386, 55.7139]) }),
            ],
          }),
        })
      );
  };
</script>

<div id={mapId} class="map" use:setupMap />
<button on:click={addLayer}>add</button>

<style>
  .map {
    width: 800px;
    height: 800px;
  }

  .map .ol-attribution {
    display: none;
  }
</style>
