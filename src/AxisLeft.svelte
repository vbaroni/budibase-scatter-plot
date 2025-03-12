<script>
  export let yScale;
  export let margin;
  export let height;
  export let yAxisTickAmount;
  export let yAxisTitle;
</script>

{#if yScale}
  <g transform="translate({margin.left},0)">
    <!-- Axis title -->
    {#if yAxisTitle}
      <text 
        class="axis-label" 
        x={-margin.top} 
        y={margin.left - 10}
        transform="rotate(-90)"
      >
        {yAxisTitle}
      </text>
    {/if}

    <!-- Axis line -->
    <line stroke="currentColor" y1={height - margin.bottom} y2={margin.top} />

    {#each yScale.ticks(yAxisTickAmount) as tick}
      {#if tick !== 0}
        <!-- Draw tick horizontal line -->
        <line
          stroke="currentColor"
          x1={0}
          y1={yScale(tick)}
          x2={-6}
          y2={yScale(tick)}
        />
      {/if}

      <text class="axis-ticks" x={-9} y={yScale(tick)}>
        {tick}
      </text>
    {/each}
  </g>
{/if}

<style>
  .axis-label {
    font-size: 18px;
    fill: currentColor;
    text-anchor: end;
  }

  .axis-ticks {
    font-size: 10px;
    text-anchor: end;
    dominant-baseline: middle;
    fill: currentColor;
  }
</style>
