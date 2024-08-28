<script>
	import { onMount } from 'svelte';
	import Hvezda from './Hvezda.svelte';
	import gsap from 'gsap';

	/**
	 * @typedef {Object} Props
	 * @property {number} [misto]
	 * @property {any} jmena
	 */
	/**@type {Props} */
	let { jmena, misto } = $props();
	jmena = jmena.split(', ');

	/**@type {HTMLImageElement[]} */
	let images = new Array(jmena.length).fill(null);

	/**
	 * @param {HTMLImageElement} element
	 * @param {number} left
	 */
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
	<div class="images p{jmena.length}">
		{#each jmena as jmeno, index}
			<a
				class="l{index * 25}"
				href="/o-nas"
				data-tooltip={jmeno.replaceAll('_', ' ')}
				style="border-bottom: none;  cursor: pointer; display: block"
			>
				<img
					src="/clenove/{jmeno}.png"
					alt={jmeno}
					style:left={index * 25 + 'px'}
					style:z-index={jmena.length - index}
					bind:this={images[index]}
				/>
			</a>
		{/each}
	</div>
	{#if misto}
		{#if misto >= 4}
			<div class="medaile m{jmena.length}">
				<Hvezda {misto} rotate={2.5 * misto} />
			</div>
		{:else}
			<div class="m{jmena.length}">
				<img src="/medaile/{misto}{jmena.length <= 4 ? 's' : 'l'}.svg" alt="" />
			</div>
		{/if}
	{/if}
</div>

<style>
	.images img {
		border-radius: 50%;
		aspect-ratio: 1;
		border: 3.5px solid black;
		height: 50px;
		object-fit: cover;
		position: absolute;
		top: 0;
		left: 0;
	}

	.skupina {
		display: grid;
		justify-content: center;
		align-items: center;
		width: 150px;
		margin-bottom: 1rem;
		.images {
			position: relative;
			max-width: 500px;
			height: 100px;
		}
	}
	img[src*='medaile'] {
		margin-top: -80px;
		width: 125px;
	}
	img[src*='l.'] {
		width: 150px;
		margin-top: -90px;
	}

	.medaile {
		margin-inline: 15px;
		margin-top: -50px;
		height: 80px;
		aspect-ratio: 1;
	}
	.medaile.m5 {
		margin-inline: 30px;
	}
	:global(div:has(div.skupina)) {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		gap: 2rem;
	}
	.p5 {
		.l0::after {
			left: 15%;
		}
		.l25::after {
			left: 35%;
		}
		.l50::after {
			left: 55%;
		}
		.l75::after {
			left: 70%;
		}
		.l100::after {
			left: 90%;
		}
	}
	.p4 {
		.l0::after {
			left: 20%;
		}
		.l25::after {
			left: 45%;
		}
		.l50::after {
			left: 65%;
		}
		.l75::after {
			left: 90%;
		}
	}
</style>
