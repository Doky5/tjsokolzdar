<script>
	import Header from '$lib/components/Header.svelte';
</script>

<Header />

<slot />

<style>
	:global(main)  {
		padding-inline: min(4rem, 10%) ;
		margin-inline: auto;
		margin-top: 2rem;
	}
	:global(*) {
		margin: 0;
		padding: 0;
	}
</style>