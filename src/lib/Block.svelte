<script lang="ts">
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();

	export let status: number;
	export let retu: number;
	export let gyou: number;

	const handleClick = () => {
		dispatch('select', {
			retu: retu,
			gyou: gyou
		});
	};
</script>

{#if status === 0}
	<button on:click={handleClick} />
{:else if status === 1}
	<div class="circle" />
{:else if status === -1}
	<div class="ex" />
{/if}

<style lang="scss">
	button {
		width: 150px;
		height: 150px;
	}

	.circle {
		width: 150px;
		height: 150px;
		border: 5px solid #000000;
		box-sizing: border-box;
		border-radius: 50%;
	}

	.ex {
		width: 150px;
		height: 150px;
		position: relative;

		&::before {
			content: '';
			display: block;
			width: 100%; /*バツ線の長さ*/
			height: 10px; /*バツ線の太さ*/
			background: #000;
			transform: rotate(45deg);
			transform-origin: 0% 50%;
			position: absolute;
			top: calc(14% - 5px);
			left: 14%;
		}

		&::after {
			content: '';
			display: block;
			width: 100%; /*バツ線の長さ*/
			height: 10px; /*バツ線の太さ*/
			background: #000;
			position: absolute;
			top: calc(14% - 5px);

			transform: rotate(-45deg);
			transform-origin: 100% 50%;
			left: auto;
			right: 14%;
		}
	}
</style>
