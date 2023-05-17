<script lang="ts">
  import { getContext, onDestroy } from "svelte";
  import { Map } from "ol";

  const { getMap } = getContext<{ getMap: () => Map }>("open-layers");
  const map = getMap();
</script>
