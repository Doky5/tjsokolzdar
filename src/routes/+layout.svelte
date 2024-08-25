<script>
	import Header from '$lib/components/Header.svelte';
</script>

<Header />

<slot />

<style>
	:global(main)  {
		margin: 30px;
	}
	:global(*) {
		margin: 0;
		padding: 0;
	}
</style>