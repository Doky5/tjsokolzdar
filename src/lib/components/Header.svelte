<script>
	import * as rive from '@rive-app/canvas';
	import { slide } from 'svelte/transition';
	import Hamburger from './Hamburger.svelte';
	import { menuOpen } from '$lib/stores.js';
	/**@type {HTMLCanvasElement} */
	let logo;
	/**@type {boolean} */
	let open = $state(false);
	menuOpen.subscribe((value) => {
		open = value; 
	});
	$effect(() => {
		console.log({open});
		const r1 = new rive.Rive({
			src: '/gymnastika.riv',
			// OR the path to a discoverable and public Rive asset
			// src: '/public/example.riv',
			canvas: logo,
			autoplay: true,
			animations: 'Timeline 1',
			onLoad: () => {
				r1.resizeDrawingSurfaceToCanvas();
			}
		});
	});
</script>

<header>
	<nav>
		<div class="logo">
			<a href="/">
				<canvas bind:this={logo} width="400" height="300"></canvas>
			</a>
		</div>

		<Hamburger />
	</nav>
	{#if open}
		<menu in:slide={{ duration: 500 }} out:slide={{ duration: 200 }}>
			<a href="/aktuality">Aktuality</a><!--Novinky v klubu -->
			<a href="/treninky">Tréninky</a><!-- Rozvrh tréninků -->
			<a href="/zavody">Závody</a><!-- Tabulka se závody - kde, kdy, doprava -->
			<a href="/o-nas">O nás</a><!-- Trenéři a gymnastky - bubliny se jmény -->
			<a href="/kontakty">Kontakty</a><!-- Tabulka s kontakty -->
		</menu>
	{/if}
</header>

<style>
	header {
		display: grid;
		menu {
			display: grid;
			padding: 0;
			a {
				background: rgb(226, 226, 226);
				padding: 20px;
				text-align: center;
			}
		}
		.logo {
			display: flex;
			canvas {
				height: 4rem;
				margin: 10px;
			}
		}

		nav {
			display: flex;
			justify-content: space-between;
			align-items: center;
		}
	}
</style>
