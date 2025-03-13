<script>
  export let yScale;
  export let margin;
  export let height;
  export let yAxisTickAmount;
  export let yAxisTitle;
  export let yAxisTopLabel;
  export let yAxisBottomLabel;
  export let axisLabelSize;
  export let axisTitleSize;
  export let axisStepSize;
</script>

{#if yScale}
  <g transform="translate({margin.left},0)">
    <!-- Axis title and labels-->
    <foreignObject
      width={height - margin.bottom - margin.top}
      height={40}
      x={-height + margin.bottom}
      y={0}
      transform="rotate(-90)"
    >
      <div class="text-container" transform="rotate(-90)">
        <div class="label" style="font-size: {axisLabelSize};">
          {yAxisBottomLabel ?? ""}
        </div>
        <div class="main-title" style="font-size: {axisTitleSize};">
          {yAxisTitle ?? ""}
        </div>
        <div class="label" style="font-size: {axisLabelSize};">
          {yAxisTopLabel ?? ""}
        </div>
      </div>
    </foreignObject>

    <!-- Axis line -->
    <line stroke="currentColor" y1={height - margin.bottom} y2={margin.top} stroke-width="3" />

    {#each yScale.ticks(yAxisTickAmount) as tick}
      {#if tick !== 0}
        <!-- Draw tick horizontal line -->
        <line
          stroke="currentColor"
          stroke-width="3"
          x1={0}
          y1={yScale(tick)}
          x2={-6}
          y2={yScale(tick)}
        />
      {/if}

      <text class="axis-ticks" x={-9} y={yScale(tick)} style="font-size: {axisStepSize};">
        {tick}
      </text>
    {/each}
  </g>
{/if}

<style>
  .axis-ticks {
    text-anchor: end;
    dominant-baseline: middle;
    fill: currentColor;
    font-family: "Space Grotesk", sans-serif;
  }

  .text-container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: start;
    height: 100%;
    padding-top: 5px;
  }

  .label {
    padding-left: 30px;
    font-weight: 500;
    font-family: "Space Grotesk", sans-serif;
  }

  .main-title {
    font-family: "Pangolin", cursive;
    font-weight: 500;
    text-transform: uppercase;
  }
</style>
