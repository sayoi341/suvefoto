<script lang="ts">
	import Block from '$lib/Block.svelte';

	let win = 0;

	let grid: number[][] = [
		[0, 0, 0],
		[0, 0, 0],
		[0, 0, 0]
	];

	let counter = 0;
	$: time = counter % 2;

	const handleSelect = (event) => {
		if (time === 0) {
			grid[event.detail.gyou][event.detail.retu] = 1;
		} else {
			grid[event.detail.gyou][event.detail.retu] = -1;
		}
		counter++;

		win = search();
		console.log(win);
	};

	const search = (): number => {
		for (let index = 0; index <= 2; index++) {
			if (grid[index][0] == grid[index][1] && grid[index][1] == grid[index][2]) {
				return grid[index][0];
			}
		}

		for (let index = 0; index <= 2; index++) {
			if (grid[0][index] == grid[1][index] && grid[1][index] == grid[2][index]) {
				return grid[0][index];
			}
		}

		if (grid[0][0] == grid[1][1] && grid[1][1] == grid[2][2]) {
			return grid[0][0];
		}

		if (grid[2][0] == grid[1][1] && grid[1][1] == grid[0][2]) {
			return grid[1][1];
		}
	};
</script>

<svelte:head>
	<title>まるばつゲーム</title>
</svelte:head>

{#each grid as line, i}
	<div class="retu">
		{#each line as state, j}
			<Block gyou={i} retu={j} status={state} on:select={handleSelect} />
		{/each}
	</div>
{/each}

{#if win === 1}
	<h1>まるの勝ちです</h1>
{:else if win === -1}
	<h1>ばつの勝ちです</h1>
{/if}

<style lang="scss">
	.retu {
		display: flex;
	}
</style>
