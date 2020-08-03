<script>
  import { ops, capitalize } from "./helpers";
  let height = 100;
  let width = 100;
  let doors = 2;
  let system = "520";

  const availableSystems = ["520", "744"];
  const availableDoors = [2, 3, 4];

  const calc = (s, w, h) => ops[s](w, h);

  $: calculatedSystem = calc(system, width, height);
  $: measures = Object.keys(calculatedSystem);
</script>

<style>
  .input {
    display: block;
    max-width: 25rem;
    margin-bottom: 1rem;
    width: 100%;
    font-size: 1.5rem;
  }
  .box {
    display: flex;
    padding: 1rem;
    flex-direction: column;
    border-radius: 8px;
    background: aliceblue;
    border: 1px solid #c5def4;
  }
</style>

<label>Ancho (cms):</label>
<input class="input" bind:value={height} placeholder={'Alto'} type="number" />
<label>Alto (cms):</label>
<input class="input" bind:value={width} placeholder={'Ancho'} type="number" />
<select class="input" bind:value={system}>
  {#each availableSystems as currentSystem}
    <option value={currentSystem}>{`Sistema ${currentSystem}`}</option>
  {/each}
</select>
<div class="box">
  <h2>
    Las medidas para una ventana {width}x{height}cms del sistema {system} son:
  </h2>
  {#each measures as measure}
    <p>{capitalize(measure)}: {calculatedSystem[measure]}cm</p>
  {/each}

</div>
