<script>
  import { getContext } from "svelte";
  import { scaleLinear, scaleSqrt } from "d3-scale";
  import AxisLeft from "./AxisLeft.svelte";
  import AxisBottom from "./AxisBottom.svelte";
  import ForeignCircle from "./ForeignCircle.svelte";
  import Shadow from "./Shadow.svelte";

  export let dataProvider;
  export let proposition;
  export let xAxisField;
  export let yAxisField;
  export let acteurs;
  export let strategies;
  export let priorite;

  export let height;
  export let width;

  export let xAxisMin;
  export let xAxisMax;
  export let xAxisStep;
  export let xAxisTitle;

  export let yAxisMin;
  export let yAxisMax;
  export let yAxisStep;
  export let yAxisTitle;

  $: data = dataProvider?.rows ?? [];
  $: xAxisTickAmount = (xAxisMax - xAxisMin) / xAxisStep ?? 10;
  $: yAxisTickAmount = (yAxisMax - yAxisMin) / yAxisStep ?? 10;

  const margin = { top: 20, right: 20, bottom: 20, left: 35 }; // Do not expose! --> If exposed, define min values!!!!!
  const diameter = 140;

  const { styleable } = getContext("sdk");
  const component = getContext("component");

  //Define X axis scale and bounds
  $: xScale = scaleLinear()
    .domain([xAxisMin, xAxisMax])
    .range([margin.left, width - margin.right]);

  //Define Y axis scale and bounds
  $: yScale = scaleLinear()
    .domain([yAxisMin, yAxisMax])
    .range([height - margin.bottom, margin.top]);

</script>

<div use:styleable={$component.styles}>
  <div class="chart-container">
    {#if data}
      <svg {width} {height}>
        <AxisLeft {yScale} {margin} {height} {yAxisTickAmount} {yAxisTitle} />
        <AxisBottom
          {xScale}
          {margin}
          {height}
          {width}
          {xAxisTickAmount}
          {xAxisTitle}
        />

        <g>
          <!-- This is done to keep shadow behind the bubbles -->
          <Shadow
            {data}
            {yScale}
            {xScale}
            {xAxisField}
            {yAxisField}
            {diameter}
            {margin}
            {xAxisMin}
            {yAxisMax}
          />

          {#each data as d, i}
            <ForeignCircle
              {d}
              {diameter}
              {yScale}
              {xScale}
              {proposition}
              {xAxisField}
              {yAxisField}
              {acteurs}
              {strategies}
              {priorite}
            />
          {/each}
        </g>
      </svg>
    {/if}
  </div>
</div>

<style>
  .chart-container {
    display: flex;
    width: 100%;
    height: 100%;
    flex-direction: column;
    align-items: center;
  }
</style>
