<script lang="ts">
  import ForceGraph3D from "3d-force-graph";
  import { onMount } from "svelte";
  import * as SC from "svelte-cubed";

  let canvasDom: HTMLElement;
  let Graph: ForceGraph3D;
  onMount(() => {
    Graph = ForceGraph3D()(canvasDom);
  });

  // Random tree
  const N = 300;
  $: if (canvasDom) {
    Graph.graphData({
      nodes: [...Array(N).keys()].map((i) => ({ id: i })),
      links: [...Array(N).keys()]
        .filter((id) => id)
        .map((id) => ({
          source: id,
          target: Math.round(Math.random() * (id - 1)),
        })),
    });
  }
</script>

<template>
  <!-- <SC.Canvas bind:this={canvasDom} /> -->
  <div class="w-screen h-screen" bind:this={canvasDom} />
</template>
