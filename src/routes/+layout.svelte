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
	:global(main .home) {
		position: relative;
		text-align: center;
		left: 0;
		width: 100%;
		aspect-ratio: 16/9;

		background-size: contain;
		background-image: url('/main.jpg');
		background-repeat: no-repeat;

		border-image: fill 1 linear-gradient(rgba(0, 0, 0, 0.255), rgba(0, 0, 0, 0.527));
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

	:global(*) {
		margin: 0;
		padding: 0;
	}
	
</style>
