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
	let matches = 0;
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
		showsCards(cardList);
		shuffleCards();
		setTimeout(showsCards(cardSet), 1000);
	});
	const showsCards = (array) => {
		for (let i = 0; i < array.length; i++) {
			array[i].b = !array[i].b;
		}
	};
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
		let cs = [];
		let i = 0;
		cardSet.forEach((c) => {
			i++;
			c = { ...c, id: i };
			cs = [...cs, c];
		});
		cardSet = cs;
		console.log(cardSet);
	};

	let q = [];
	const butt = (n) => {
		q = [...q, n];
		if (q.length > 1) {
			if (q[0].n === q[1].n) {
				matches++;
			} else {
				const i = q[0].id;
				const i2 = q[1].id;
				setTimeout(() => {
					cardSet[i - 1].b = false;
					cardSet[i2 - 1].b = false;
				}, 1000);
				err++;
			}
		}
		if (q.length == 2) {
			q = [];
		}
		console.log(q);
	};
	const reset = () => {
		for (let i = 0; i < cardSet.length; i++) {
			cardSet[i].b = false;
			err = 0;
			matches = 0;
		}
	};
</script>

<h2>Errors: <span id="errors">{err}</span> Matches: <span id="matches">{matches}</span></h2>
<div id="board" bind:this={board}>
	{#if cardSet}
		{#each cardSet as c}
			{#if c.b}<button><img class="card" src={c.n} alt="" srcset="" /></button>{:else}<button
					on:click={() => {
						c.b = !c.b;
						butt({ id: c.id, n: c.n });
					}}
				>
					<img class="card" src={back} alt="" />
				</button>{/if}
		{/each}
	{/if}
</div>
<button id="butt" on:click={reset}>Reset</button>

<style>
	h2 {
		padding: 1rem;
	}
	#errors {
		color: red;
	}
	#matches {
		color: green;
	}
	#butt {
		width: 400px;
		background-color: red;
		font-size: 50px;
	}
</style>
