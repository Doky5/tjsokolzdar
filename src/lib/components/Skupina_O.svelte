<script>
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	/**@type {any}*/
	let { jmena } = $props();
	jmena = jmena.split(', ');

	/**@type {HTMLImageElement[]} */
	let images = new Array(jmena.length).fill(null);

	onMount(() => {
		images.forEach((img, index) => {
			img.addEventListener('mouseenter', () => {
				images.forEach((img, i) => {
					if (i != index) {
						gsap.to(img, {
							x: i > index ? 20 : -20,
							scale: 0.8,
							ease: 'bounce.out',
							duration: 0.7
						});
					}
				});
			});

			img.addEventListener('mouseleave', () => {
				images.forEach((image) => {
					gsap.killTweensOf(image);
					gsap.to(image, { x: 0, scale: 1 });
				});
			});
		});
	});
</script>

<div class="skupina">
	{#each jmena as jmeno, index}
		<a
			style:left={index * -15 + 'px'}
			href="/o-nas"
			data-tooltip={jmeno.replaceAll('_', ' ')}
			style="border-bottom: none;  cursor: pointer; "
		>
			<img
				src="/clenove/{jmeno}.png"
				alt={jmeno}
				style:z-index={jmena.length - index}
				bind:this={images[index]}
			/>
		</a>
	{/each}
</div>

<style>
	img {
		border-radius: 50%;
		border: 3.5px solid black;
		height: 50px;
		object-fit: cover;
		position: absolute;
	}
	a {
		top: 0;
		left: 0;
		width: 50px;
		aspect-ratio: 1;
        display: inline-block;
	}

	.skupina {
		margin-bottom: 1rem;

		position: relative;
	}
	
</style>
