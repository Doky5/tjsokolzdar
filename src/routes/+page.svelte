<script>
	import { fade, fly } from 'svelte/transition';
	import Domu from '../content/Domu.md';
	import gsap from 'gsap';
	import { onMount, tick } from 'svelte';
	onMount(() => {
		gsap.fromTo(
		   ".home h1",
			 {y: 50, opacity: 0 },
			 {y: 0, opacity: 1,delay: 0.5}
		);
	});
</script>

<main in:fade>
	<div class='home'>
		<h1>Domovská stránka beta</h1>
	</div>
	<article>
		<Domu />
	</article>
</main>
