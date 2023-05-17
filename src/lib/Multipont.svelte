<script lang="ts">
  import { getContext, onDestroy } from "svelte";
  import { Vector } from "ol/source";
  import { Map } from "ol";
  import VectorLayer from "ol/layer/Vector";
  import { MultiPoint } from "ol/geom";
  import { Feature } from "ol";
  import { Style, Icon } from "ol/style";

  const { getMap } = getContext<{ getMap: () => Map }>("open-layers");
  const map = getMap();
  const multipoint_layer = new VectorLayer({
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
  });
  map.addLayer(multipoint_layer);

  onDestroy(() => map.removeLayer(multipoint_layer));
</script>

<slot />
