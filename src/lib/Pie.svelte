<script>
  import * as d3 from 'd3';
  
let arcGenerator = d3.arc().innerRadius(0).outerRadius(50);

let data = [
	{ value: 1, label: "apples" },
	{ value: 2, label: "oranges" },
	{ value: 3, label: "mangos" },
	{ value: 4, label: "pears" },
	{ value: 5, label: "limes" },
	{ value: 5, label: "cherries" }
];

let sliceGenerator = d3.pie().value(d => d.value);

    let arcData = sliceGenerator(data);
    let arcs = arcData.map(d => arcGenerator(d));
let colors = d3.scaleOrdinal(d3.schemeTableau10);

</script>

<div>This is a Pie chart!</div>

<ul>
	{#each data as d}
		{#if d > 15}
			<li><strong>{d}</strong></li>
		{:else}
			<li>{d}</li>
		{/if}
	{/each}
</ul>

<div class="container">
<svg viewBox="-50 -50 100 100">
{#each arcs as arc, index}
  <path d={ arc } fill={ colors(index) } />
{/each}

</svg>
<ul class="legend">
	{#each data as d, index}
		<li style="--color: { colors(index) }">
			<span class="swatch"></span>
			{d.label} <em>({d.value})</em>
		</li>
	{/each}
</ul>
</div>

<style>
svg {
	max-width: 20em;
	margin-block: 2em;

	/* Do not clip shapes outside the viewBox */
	overflow: visible;
}
.container {
    display: flex;

}
</style>