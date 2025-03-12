<script>
  export let xScale;
  export let margin;
  export let height;
  export let width;
  export let xAxisTickAmount;
  export let xAxisTitle;
</script>

{#if xScale}
  <g transform="translate(0,{height - margin.bottom})">
    {#if xAxisTitle}
      <!-- Axis title -->
      <text class="axis-label" x={width - margin.right} y={-10}>
        {xAxisTitle}
      </text>
    {/if}

    <!-- Axis line -->
    <line stroke="currentColor" x1={margin.left} x2={width - margin.right} />

    <!-- Ticks -->
    {#each xScale.ticks(xAxisTickAmount) as tick}
      <line
        stroke="currentColor"
        x1={xScale(tick)}
        y1={0}
        x2={xScale(tick)}
        y2={6}
      />

      <text class="axis-ticks" x={xScale(tick)} y={16}>
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
    text-anchor: middle;
    dominant-baseline: middle;
    fill: currentColor;
  }
</style>
