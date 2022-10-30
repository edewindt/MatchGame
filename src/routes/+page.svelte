<script>
	import { onMount } from 'svelte';
	import darkness from '$lib/darkness.jpg';
	import double from '$lib/double.jpg';
	import fighting from '$lib/fighting.jpg';
	import fairy from '$lib/fairy.jpg';
	import fire from '$lib/fire.jpg';
	import grass from '$lib/grass.jpg';
	import lightning from '$lib/lightning.jpg';
	import metal from '$lib/metal.jpg';
	import psychic from '$lib/psychic.jpg';
	import water from '$lib/water.jpg';
	import back from '$lib/back.jpg';
	let err = 0;
	let board;
	let cardList = [
		{ n: darkness, b: false },
		{ n: double, b: false },
		{ n: fairy, b: false },
		{ n: fighting, b: false },
		{ n: fire, b: false },
		{ n: grass, b: false },
		{ n: lightning, b: false },
		{ n: metal, b: false },
		{ n: psychic, b: false },
		{ n: water, b: false }
	];
	let cardSet;
	let boardc = [];
	onMount(() => {
		shuffleCards();
	});

	const shuffleCards = () => {
		let cardSet1 = [];
		let cardSet2 = [];
		cardList.forEach((c) => {
			c = { ...c, list: 1 };
			cardSet1 = [...cardSet1, c];
		});
		cardList.forEach((c) => {
			c = { ...c, list: 2 };
			cardSet2 = [...cardSet2, c];
		});
		console.log(cardSet1);
		console.log(cardSet2);
		cardSet = cardSet1.concat(cardSet2); // Doubling cards
		console.log(cardSet);
		//Shuffle cards
		for (let i = 0; i < cardSet.length; i++) {
			let j = Math.floor(Math.random() * cardSet.length); // Random index
			//Swap
			let temp = cardSet[i];
			cardSet[i] = cardSet[j];
			cardSet[j] = temp;
		}
		console.log(cardSet);
	};
</script>

<h2>Errors: <span id="errors">{err}</span></h2>
<div id="board" bind:this={board}>
	{#if cardSet}
		{#each cardSet as c}
			{#if c.b}<button
					on:click={() => {
						c.b = !c.b;
					}}><img class="card" src={c.n} alt="" srcset="" /></button
				>{:else}<button
					on:click={() => {
						c.b = !c.b;
					}}
				>
					<img class="card" src={back} alt="" />
				</button>{/if}
		{/each}
	{/if}
</div>
