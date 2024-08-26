<script>
	/**
	 * @typedef {Object} Props
	 * @property {number} misto
	 * @property {number} rotate
	 * @property {number} [t_size]
	 */

	/** @type {Props} */
	let { misto, rotate, t_size } = $props();
</script>

<div class="hvezda">
	<img
		class:rotate
		style={`animation-duration: ${rotate}s;`}
		src="/medaile/hvezda.svg"
		alt="{misto}. místo"
	/>
	<p style:font-size={t_size + 'rem'}>{misto}</p>
</div>

<style>
	.hvezda {
		position: relative;
        aspect-ratio: 1;
	}
	p {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		font-size: 1.5rem;
		color: white;
	}
	.rotate {
		animation: rotate 30s infinite linear;
	}
	@keyframes rotate {
		from {
			transform: rotate(0deg);
		}
		to {
			transform: rotate(360deg);
		}
	}
</style>
