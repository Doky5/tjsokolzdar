<script>
	import { fade } from 'svelte/transition';
	import Kontakty from '../../content/Kontakty.mdx';
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
        :global(& + p) {
            margin-top: 50px;
        }
	}
	article :global(div) {
		display: flex;
		justify-content: space-between;
        align-items: center;
		margin: 1rem 2rem;
	}
</style>
