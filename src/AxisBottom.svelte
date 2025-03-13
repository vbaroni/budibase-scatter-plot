<script>
  export let xScale;
  export let margin;
  export let height;
  export let width;
  export let xAxisTickAmount;
  export let xAxisTitle;
  export let xAxisLeftLabel;
  export let xAxisRightLabel;
  export let axisLabelSize;
  export let axisTitleSize;
  export let axisStepSize;
</script>

{#if xScale}
  <g transform="translate(0,{height - margin.bottom})">
    <!-- Axis title and labels-->
    <foreignObject
      width={width - margin.right - margin.left}
      height={40}
      x={margin.left}
      y={-margin.bottom - margin.top}
    >
      <div class="text-container">
        <div class="label" style="font-size: {axisLabelSize};">
          {xAxisLeftLabel ?? ""}
        </div>
        <div class="main-title" style="font-size: {axisTitleSize};">
          {xAxisTitle ?? ""}
        </div>
        <div class="label" style="font-size: {axisLabelSize};">
          {xAxisRightLabel ?? ""}
        </div>
      </div>
    </foreignObject>

    <!-- Axis line -->
    <line stroke="currentColor" x1={margin.left} x2={width - margin.right} stroke-width="3"/>

    <!-- Ticks -->
    {#each xScale.ticks(xAxisTickAmount) as tick}
      <line
        stroke="currentColor"
        stroke-width="3"
        x1={xScale(tick)}
        y1={0}
        x2={xScale(tick)}
        y2={6}
      />

      <text class="axis-ticks" x={xScale(tick)} y={16} style="font-size: {axisStepSize};">
        {tick}
      </text>
    {/each}
  </g>
{/if}

<style>
  .axis-ticks {
    text-anchor: middle;
    dominant-baseline: middle;
    fill: currentColor;
    font-family: "Space Grotesk", sans-serif;
  }

  .text-container {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: end;
    height: 100%;
    padding-bottom: 5px;
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
