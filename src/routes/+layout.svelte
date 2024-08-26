<script>
	import Header from '$lib/components/Header.svelte';
</script>

<Header />

<slot />

<style>
	:global(main) {
		margin-inline: auto;
		margin-top: 1rem;
	}
	:global(*) {
		margin: 0;
		padding: 0;
	}
	
</style>
