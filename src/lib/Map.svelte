<script lang="ts">
  import { onDestroy, setContext } from "svelte";
  import { Map } from "ol";
  import TileLayer from "ol/layer/Tile";
  import Stamen from "ol/source/Stamen";
  import View from "ol/View";
  import { useGeographic } from "ol/proj";

  useGeographic();

  let map: Map = null;

  const setupMap = (node) => {
    const osmLayer = new TileLayer({
      source: new Stamen({ layer: "toner-lite" }),
    });
    map = new Map({
      target: node.id,
      layers: [osmLayer],
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
          map.setTarget(null);
          map = null;
        }
      },
    };
  };

  $: map && console.log(map.getLayers().getArray());

  setContext("open-layers", {
    getMap: (): Map => map,
  });
</script>

<div class="map" id="map-container" use:setupMap>
  {#if map}
    <slot />
  {/if}
</div>

<style>
  .map {
    width: 800px;
    height: 800px;
  }
</style>
