<script>
	//@ts-nocheck
	import { onMount } from 'svelte';

	let disabled_L = true,
		disabled_R = false;
	// Import all images in the 'galerie' folder eagerly
	let images = import.meta.glob('../../../static/galerie/*.jpg', { eager: true });

	// Extract and format image paths for use in the gallery
	const paths = Object.keys(images).map((path) =>
		path.replace('../../../static/galerie/', '/galerie/')
	);

	onMount(() => {
		// Make the first image visible on mount
		const firstImage = document.querySelector('.gallery img');
		if (firstImage) firstImage.classList.add('visible');
	});

	function previous() {
		const current = document.querySelector('.gallery img.visible');
		if (current) {
			const previous = current.previousElementSibling;
			if (previous && previous.tagName === 'IMG') {
				current.classList.remove('visible', 'slide-in-left', 'slide-in-right');
				current.classList.add('slide-out-right');
				previous.classList.remove('slide-out-right', 'slide-out-left');
				previous.classList.add('visible', 'slide-in-left');
				if (!previous.previousElementSibling || previous.previousElementSibling.tagName !== 'IMG' ) {
					disabled_L = true;
				} else {
					disabled_L = false;
				}
			}
		}
	}

	function next() {
		const current = document.querySelector('.gallery img.visible');
		if (current) {
			const next = current.nextElementSibling;
			if (next && next.tagName === 'IMG') {
				current.classList.remove('visible', 'slide-in-left', 'slide-in-right');
				current.classList.add('slide-out-left');
				next.classList.remove('slide-out-right', 'slide-out-left');
				next.classList.add('visible', 'slide-in-right');
				if (!next.nextElementSibling || next.nextElementSibling.tagName !== 'IMG' ) {
					disabled_R = true;
				} else {
					disabled_R = false;
				}
			}
		}
	}
</script>

<!-- svelte-ignore css_unused_selector -->
<div class="gallery">
	{#each paths as path}
		<img src={path} alt="" />
	{/each}
	<button
		on:click={(disabled_R = false)}
		on:click={previous}
		class="nav-button left"
		class:disabled_L>&lt;</button
	>
	<button on:click={(disabled_L = false)} on:click={next} class="nav-button right" class:disabled_R
		>&gt;</button
	>
</div>

<style>
	.gallery {
		position: relative;
		width: 100%;
		height: 700px;
		background: rgba(32, 32, 32, 0.918);
        border-radius: 10px;
		margin: 0;
		padding: 0;
		overflow: hidden; /* Prevents images from showing outside of gallery area */
	}
	.gallery img {
		position: absolute;
		max-width: 600px;
		max-height: 700px;
		width: 100%;
		height: auto;
		object-fit: contain;
		border-radius: 20px;
		opacity: 0;
		transition:
			transform 0.5s ease,
			opacity 0.5s ease;
		inset: 0;
		margin: auto;
		transform: translateX(100%); /* Start position off-screen right */
	}
	:global(.gallery img.visible) {
		opacity: 1;
		transform: translateX(0); /* Slide in from right */
	}

	:global(.gallery img.slide-out-left) {
		transform: translateX(-100%); /* Slide out to left */
	}
	:global(.gallery img.slide-out-right) {
		transform: translateX(100%); /* Slide out to right */
	}
	.nav-button {
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		color: #fff;
		background: none;
		border: none;
		padding: 10px;
		cursor: pointer;
		font-size: 20px;
	}
	.disabled_L {
		color: gray;
        cursor: not-allowed;
	}
	.disabled_R {
		color: gray;
        cursor: not-allowed;
	}
	.nav-button.left {
		left: 10px;
	}
	.nav-button.right {
		right: 10px;
	}
</style>
