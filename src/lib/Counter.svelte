<script lang="ts">
  import { shuffle } from "fast-shuffle";
  import { flip } from "svelte/animate";

  let list: Array<number> = [3, 4, 5, 6];
  const shuffle_list = () => {
    list = shuffle(list);
  };
</script>

<div
  on:keydown={shuffle_list}
  on:click={shuffle_list}
  class="max-w-[400px] m-auto"
>
  {import.meta.env.MODE}
  {#each list as item (item)}
    <div
      animate:flip={{ duration: 500 }}
      class="bg-slate-900 w-10 h-10 rounded-md p-2 m-2"
    >
      <p class="font-semibold text-lg text-white">{item}</p>
    </div>
  {/each}
</div>
