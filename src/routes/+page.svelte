<script>
	import { fade, fly } from 'svelte/transition';
	import Domu from '../content/Domu.mdx';
	import gsap from 'gsap';
	let before = true;
	import { ScrollTrigger } from 'gsap/dist/ScrollTrigger.js';

	// register ScrollTrigger
	import { onMount } from 'svelte';
	onMount(() => {
		gsap.registerPlugin(ScrollTrigger);

		gsap.fromTo('.home h1', { y: 50, opacity: 0 }, { y: 0, opacity: 1, delay: 0.5 });

		document.querySelectorAll('article > div').forEach((div) => {
			// @ts-ignore
			ScrollTrigger.create({
				trigger: div,
				start: 'top 80%',
				animation: gsap.fromTo(div, { y: 30, opacity: 0 }, { y: 0, opacity: 1 })
			});
		});
		setTimeout(() => {
			before = false;
		}, 2000);
	});
</script>

<main in:fade>
	<div class="home" class:before>
		<h1>Domovská stránka beta</h1>
	</div>
	<article>
		<Domu />
	</article>
</main>

<style>
	main .home {
		position: relative;
		text-align: center;
		left: 0;
		width: 100%;
		aspect-ratio: 16/9;

		background-size: contain;
		background-image: url('/main.jpg');
		background-repeat: no-repeat;
		transition: 1s;
		border-image: fill 1 linear-gradient(rgba(0, 0, 0, 0.264), rgba(0, 0, 0, 0.232));

		&.before {
			border-image: fill 1 linear-gradient(rgba(0, 0, 0, 0.564), rgba(0, 0, 0, 0.832));
		}
	}
</style>
