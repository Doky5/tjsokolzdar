<script>
	import Header from '$lib/components/Header.svelte';
</script>

<Header />

<slot />

<style>
	:global(main)  {
		width: min(100% - 4rem, 1200px);
		margin-inline: auto;
		margin-top: 2rem;
	}
	:global(*) {
		margin: 0;
		padding: 0;
	}
</style>