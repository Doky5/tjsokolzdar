<script>
	import { fade } from 'svelte/transition';
	import Kontakty from '../../content/Kontakty.md';
</script>

<main in:fade>
	<article>
		<Kontakty />
	</article>
</main>

<style>
	article :global(img[alt*='logo']) {
		width: 40px;
		:global(&[alt*='Facebook']) {
			transform: scale(120%);
		}
	}
	article :global(div) {
		display: flex;
        justify-content: space-between;
        margin: 1rem 2rem;
	}
</style>
