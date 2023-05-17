<script lang="ts">
  import Map from "./lib/Map.svelte";
  import Multipont from "./lib/Multipont.svelte";

  let show = false;
</script>

<Map>
  {#if show}
    <Multipont><h1>kid</h1></Multipont>
  {/if}
</Map>
<button on:click={() => (show = !show)}>toggle</button>
