<script>
  import chartjs from "chart.js/auto";
  import { onMount } from "svelte";
  import App from "../App.svelte";

  export let options;
  export let clss;

  let ctx;
  let chartCanvas;
  let canvas;

  onMount(async (promise) => {
    ctx = chartCanvas.getContext("2d");
    canvas = new chartjs(ctx, options);
  });

  $: if (options) {
    if (canvas) {
      ctx = chartCanvas.getContext("2d");
      canvas.destroy();
      canvas = new chartjs(ctx, options);
    }
  }
</script>

<div class="relative h-60 w-60">
  <canvas bind:this={chartCanvas} id="pie-chart" />
</div>
