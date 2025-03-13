<script>
  import Icons from "./Icons.svelte";
  import { acteursMap, strategiesMap } from "./Mappings";

  export let d;
  export let yScale;
  export let xScale;
  export let proposition;
  export let xAxisField;
  export let yAxisField;
  export let acteurs;
  export let strategies;
  export let priorite;
  export let diameter;
  export let iconSize;
  export let prioriteFontSize;
  export let propositionFontSize;
  export let strategieFontSize;

  $: centerX = xScale(+d[xAxisField]);
  $: centerY = yScale(+d[yAxisField]);
</script>

<g
  transform="translate(
          {centerX}, 
          {centerY}}
      )"
>
  <foreignObject
    width={diameter}
    height={diameter}
    x={centerX - diameter / 2}
    y={centerY - diameter / 2}
  >
    <div class="main-container">
      <div class="priorite" style="font-size: {prioriteFontSize};">
        {d[priorite]}
      </div>

      <div class="proposition" style="font-size: {propositionFontSize};">
        {d[proposition]}
      </div>

      <div
        class="strategies-container"
        style="max-height: {2 * strategieFontSize + 16};"
      >
        {#each d[strategies] as strategie}
          <span
            class="strategie"
            style="
                  color:{strategiesMap[strategie]};
                  border-color:{strategiesMap[strategie]};
                  font-size:{strategieFontSize};"
          >
            {strategie}
          </span>
        {/each}
      </div>

      <div class="acteurs-container">
        {#each d[acteurs] as acteur}
          <div class="acteur">
            <Icons name={acteursMap[acteur]} size={iconSize} />
          </div>
        {/each}
      </div>
    </div>
  </foreignObject>
</g>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300..700&display=swap");

  .main-container {
    background: white;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: center;
    display: flex;

    height: 100%;
    width: 100%;

    font-family: "Space Grotesk", sans-serif;
    color: black;

    border-radius: 50%;

    padding: 10px;
  }

  .priorite {
    font-weight: 300;
    margin-bottom: 3px;
  }

  .proposition {
    font-weight: 500;
    margin-bottom: 5px;
    text-align: center;

    overflow: hidden;
    max-height: 100%;
    text-overflow: ellipsis;
  }

  .strategies-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 3px;
  }

  .strategie {
    font-weight: 400;
    border: 1px solid;
    border-radius: 10px;
    padding: 1px 3px;
    margin-bottom: 2px;
  }

  .acteurs-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin-bottom: 3px;
  }

  .acteur {
    margin-right: 4px;
  }
</style>
