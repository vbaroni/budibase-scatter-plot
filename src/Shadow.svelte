<script>
  import { colorZone } from "./Mappings";

  export let data;
  export let yScale;
  export let xScale;
  export let xAxisField;
  export let yAxisField;
  export let diameter;
  export let margin;
  export let xAxisMin;
  export let yAxisMax;
</script>

<g>
  <defs>
    <filter id="blur">
      <feGaussianBlur in="SourceGraphic" stdDeviation="15" />
    </filter>

    <radialGradient id="circle-gradient" cx="50%" cy="50%" r="50%">
      <stop offset="0%" stop-color="white" />
      <stop offset="100%" stop-color="black" stop-opacity="1%" />
    </radialGradient>

    <mask id="circle-mask">
      {#each data as d}
        <circle
          cx={xScale(+d[xAxisField])}
          cy={yScale(+d[yAxisField])}
          r={diameter}
          fill="url(#circle-gradient)"
        />
      {/each}
    </mask>
  </defs>

  <!-- Lower left zone -->
  <rect
    x={xScale(0)}
    y={yScale(50)}
    width={xScale(50 + xAxisMin) - margin.left}
    height={yScale(-50 + yAxisMax) - margin.bottom}
    fill={colorZone.lowerLeft}
    filter="url(#blur)"
    mask="url(#circle-mask)"
  />
  <!-- Lower right zone -->
  <rect
    x={xScale(50)}
    y={yScale(50)}
    width={xScale(50 + xAxisMin) - margin.left}
    height={yScale(-50 + yAxisMax) - margin.bottom}
    fill={colorZone.lowerRight}
    filter="url(#blur)"
    mask="url(#circle-mask)"
  />
  <!-- Upper left zone -->
  <rect
    x={xScale(0)}
    y={yScale(100)}
    width={xScale(50 + xAxisMin) - margin.left}
    height={yScale(-50 + yAxisMax) - margin.bottom}
    fill={colorZone.upperLeft}
    filter="url(#blur)"
    mask="url(#circle-mask)"
  />
  <!-- Upper right zone -->
  <rect
    x={xScale(50)}
    y={yScale(100)}
    width={xScale(50 + xAxisMin) - margin.left}
    height={yScale(-50 + yAxisMax) - margin.bottom}
    fill={colorZone.upperRight}
    filter="url(#blur)"
    mask="url(#circle-mask)"
  />
</g>
