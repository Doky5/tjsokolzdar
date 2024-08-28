<script>
	import Header from '$lib/components/Header.svelte';
</script>

<Header />

<slot />

<style>
	:global(main) {
		margin-inline: auto;
		margin-top: 1rem;

		display: grid;
		padding: 0;
	}
	:global(main h1) {
		margin: 50px;
	}
	
	:global(main .home h1) {
		padding-top: 10%;
		color: white;
	}
	:global(article) {
		max-width: 1000px;
		width: 100%;
		margin-inline: auto;
	}
	:global(.bg1) {
		background: #d4d4d4;
	}
	:global(.bg2) {
		background: #bfbfbf;
	}

	:global(*) {
		margin: 0;
		padding: 0;
	}
	
</style>
