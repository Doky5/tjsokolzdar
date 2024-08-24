<script>
	import { onNavigate } from '$app/navigation';
	import * as rive from '@rive-app/canvas';
	/**@type {HTMLCanvasElement} */
	let ham;
	/**@type {boolean} */
	let open = $state(false);
	import { menuOpen } from '$lib/stores';
	menuOpen.subscribe((value) => {
		open = value;
		console.log('subscribed');
	});
	$effect(() => {
		const r2 = new rive.Rive({
			src: '/menu_gymnastika.riv',
			canvas: ham,
			autoplay: true,
			stateMachines: 'State Machine 1',
			onLoad: () => {
				r2.resizeDrawingSurfaceToCanvas();
				const inputs = r2.stateMachineInputs('State Machine 1');
				const triggerInput = inputs.find((input) => input.name === 'Boolean 1');
				console.log('loaded');
				if (triggerInput) {
					menuOpen.subscribe((value) => {
						triggerInput.value = value;
						console.log('gem mine open');
					});
				}
			}
		});
	});
	onNavigate(() => {
		menuOpen.update(() => false);
		console.log('navigated');
	});
	function handle() {
		console.log('clicked');
		menuOpen.update(() => !open);
	}
</script>

<button class="hamburger">
	<canvas bind:this={ham} onclick={handle} width="300" height="300"></canvas>
</button>

<style>
	.hamburger {
		display: flex;
		padding: 0;
		margin-right: 20px;
		border: none;
		canvas {
			height: 4rem;
			margin: 10px;
			margin: 0;
		}
	}
</style>
