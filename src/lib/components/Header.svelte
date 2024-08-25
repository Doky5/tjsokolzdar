<script>
	import * as rive from '@rive-app/canvas';
	import { slide } from 'svelte/transition';
	import Hamburger from './Hamburger.svelte';
	import { menuOpen } from '$lib/stores.js';
	import { onMount } from 'svelte';
	/**@type {HTMLCanvasElement} */
	let logo;
	/**@type {boolean} */
	let open = $state(false);
	menuOpen.subscribe((value) => {
		open = value;
	});
	onMount(() => {
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

		<div class="hamburger">
			<Hamburger />
		</div>
	</nav>
	{#key open}
		<menu
			class:open
			class:closed={!open}
			in:slide={{ duration: 500 }}
			out:slide={{ duration: 200 }}
		>
			<a href="/aktuality">Aktuality</a><!--Novinky v klubu -->
			<a href="/treninky">Tréninky</a><!-- Rozvrh tréninků -->
			<a href="/zavody">Závody</a><!-- Tabulka se závody - kde, kdy, doprava -->
			<a href="/o-nas">O nás</a><!-- Trenéři a gymnastky - bubliny se jmény -->
			<a href="/kontakty">Kontakty</a><!-- Tabulka s kontakty -->
		</menu>
	{/key}
</header>

<style>
	canvas {
		max-height: 4rem;
	}
	menu {
		display: grid;
		background: #e7e7e7;
		a {
			padding: 1rem 2rem;
			border-bottom: solid rgb(196, 196, 196) 2px;
		}
	}
	.closed {
		display: none;
	}
	.logo {
		margin-left: 20px;
	}
	@media (width > 720px) {
		header {
			display: flex;
			justify-content: space-between;
			align-items: center;
		}
		menu {
			display: flex !important;
			gap: 40px;
			margin-right: 40px;
			background: none;
			a {
				border-bottom: none;
				padding: 0;
			}
		}
		.hamburger {
			opacity: 0;
			position: absolute;
			pointer-events: none;
		}
	}
</style>
