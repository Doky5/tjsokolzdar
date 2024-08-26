<script>
	import Hvezda from './Hvezda.svelte';

	/**@type {string}*/
	export let jmeno;
	let p_jmeno = jmeno.replaceAll('_', ' ');
	/**@type {number}*/
	export let misto;
</script>

<div class="place">
	<a href="/o-nas"
		data-tooltip="{p_jmeno}"
		style="
			border-bottom: none; 
			cursor: pointer;"
	>
		<img src="/clenove/{jmeno}.png" alt={jmeno} />
	</a>
	{#if misto >= 4}
		<div class="hvezda">
			<Hvezda {misto} rotate={2.5 * misto} t_size={1} />
		</div>
	{:else}
		<img src="/medaile/{misto}.svg" alt="{misto}.místo" />
	{/if}

	<p>{p_jmeno}</p>
</div>

<style>
	img:nth-child(1) {
		border-radius: 50%;
		aspect-ratio: 1;
		border: 5px solid black;
		height: 80px;
		object-fit: cover;
	}
	.hvezda {
		height: 50px;
		aspect-ratio: 1;
		margin-top: -15px;
	}
	img[src*='medaile'] {
		position: absolute;
		height: 100px;
		margin-top: 40px;
		& + p {
			margin-top: 70px;
		}
	}
	div.place {
		display: grid;
		justify-items: center;
		max-width: 150px;
	}
	:global(div:has(div.place)) {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		gap: 2rem;
	}
	p {
		font-size: small;
	}
</style>
