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
	let err = 0;
	let board;
	let cardList = [darkness, double, fairy, fighting, fire, grass, lightning, metal, psychic, water];
	let cardSet;
	let boardc = [];
	onMount(() => {
		shuffleCards();
	});

	const shuffleCards = () => {
		cardSet = cardList.concat(cardList); // Doubling cards
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
			<img class="card" src={c} alt="" srcset="" />
		{/each}
	{/if}
</div>
