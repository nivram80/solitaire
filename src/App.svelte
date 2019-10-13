<script>
	import { deck } from "./utilities/deck";
	import Pile from "./Pile.svelte";
	import Card from "./Card.svelte";

	let shuffledDeck = [];
	let stockPile = [];

	let firstPile = [];
	let secondPile = [];
	let thirdPile = [];
	let fourthPile = [];
	let fifthPile = [];
	let sixthPile = [];
	let seventhPile = [];

	const deal = (shuffledDeck) => {
		let firstPileTemp = [];
		let secondPileTemp = [];
		let thirdPileTemp = [];
		let fourthPileTemp = [];
		let fifthPileTemp = [];
		let sixthPileTemp = [];
		let seventhPileTemp = [];

		stockPile = shuffledDeck;
		let pileNumber = 1;
		let card = {};
		while (seventhPileTemp.length < 7) {
			switch (pileNumber) {
				case 1:
					if (firstPileTemp.length < 1) {
						card = stockPile.shift();
						firstPileTemp.push(card);
						++pileNumber;
						card.visable = true;
						break;
					}
				case 2:
					if (secondPileTemp.length < 2) {
						card = stockPile.shift();
						secondPileTemp.push(card);
						++pileNumber;
						if (secondPileTemp.length === 2) {
							card.visable = true;
						}
						break;
					}
				case 3:
					if (thirdPileTemp.length < 3) {
						card = stockPile.shift();
						thirdPileTemp.push(card);
						++pileNumber;
						if (thirdPileTemp.length === 3) {
							card.visable = true;
						}
						break;
					}
				case 4:
					if (fourthPileTemp.length < 4) {
						card = stockPile.shift();
						fourthPileTemp.push(card);
						++pileNumber;
						if (fourthPileTemp.length === 4) {
							card.visable = true;
						}
						break;
					}
				case 5:
					if (fifthPileTemp.length < 5) {
						card = stockPile.shift();
						fifthPileTemp.push(card);
						++pileNumber;
						if (fifthPileTemp.length === 5) {
							card.visable = true;
						}
						break;
					}
				case 6:
					if (sixthPileTemp.length < 6) {
						card = stockPile.shift();
						sixthPileTemp.push(card);
						++pileNumber;
						if (sixthPileTemp.length === 6) {
							card.visable = true;
						}
						break;
					}
				case 7:
					if (seventhPileTemp.length < 7) {
						card = stockPile.shift();
						seventhPileTemp.push(card);
						pileNumber = 1;
						if (seventhPileTemp.length === 7) {
							card.visable = true;
						}
						break;
					}
			} 
		}
		firstPile = firstPileTemp;
		secondPile = secondPileTemp;
		thirdPile = thirdPileTemp;
		fourthPile = fourthPileTemp;
		fifthPile = fifthPileTemp;
		sixthPile = sixthPileTemp;
		seventhPile = seventhPileTemp;
	}
	
	const newDeal = () => {
		shuffledDeck = shuffle(deck);
		deal(shuffledDeck);
	}

	// Borrowed from https://javascript.info/task/shuffle which is based 
	// on https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle.
  const shuffle = (deck) => {
    for (let i = deck.length - 1; i > 0; i--) {
      let j = Math.floor(Math.random() * (i + 1));
      [deck[i], deck[j]] = [deck[j], deck[i]];
    }
    return deck;
  }
</script>

<style>
	:global(html, body) {
		margin: 0;
		padding: 0;
	}

	.header {
		display: flex;
		flex-direction: row;
		justify-content: flex-start;
		align-items: center;
		width: 100%;
		height: 60px;
		padding: 0 8px;
		background-color: black;
	}

	.title {
		width: 33%;
	}

	.actions {
		-webkit-appearance: none;
		display: flex;
		flex-direction: row;
		justify-content: flex-end;
		width: 66%;
		padding-right: 16px;
	}

	h1 {
		margin: 0;
		padding: 0;
		color: white;
	}

	.main {
		display: grid;
		grid-template-areas: "foundation tableau";
		grid-template-columns: 100px 1fr;
	}

	:global(button) {
		-webkit-appearance: none;
		width: auto;
		min-width: 100px;
		height: 32px;
		color: white;
		font-size: 13px;
		background-color: rgb(181, 3, 3);
		border: none;
		margin: 0;
		padding: 4px 8px;
		cursor: pointer;
	}

	.foundations {
		grid-area: foundation;
		display: grid;
		flex-direction: column;
		justify-content: center;
		align-items: flex-start;
		padding: 8px 0;
	}

	.foundation {
		margin-bottom: 12px;
    box-sizing: border-box;
    width: 80px;
    height: 120px;
    border-radius: 4px;
		border: 4px solid rgba(0, 0, 0, 0.10);
    padding: 4px 6px;
		font-size: 80px;
		color: rgba(0, 0, 0, 0.10);
		text-align: center;
	}

	.tableau {
		grid-area: tableau;
		display: grid;
		grid-template-columns: repeat(7, 100px);
		padding: 8px 16px;
	}
</style>

<header class="header">
	<div class="title">
		<h1>Solitaire</h1>
	</div>
	<div class="actions">
		<button on:click={newDeal}>New deal</button>
	</div>
</header>

<main class="main">
	<section class="foundations">
		<div class="foundation diamond-foundation">A</div>
		<div class="foundation heart-foundation">A</div>
		<div class="foundation club-foundation">A</div>
		<div class="foundation spade-foundation">A</div>
	</section>

	<section class="tableau">
		<Pile cards={firstPile} />
		<Pile cards={secondPile} />
		<Pile cards={thirdPile} />
		<Pile cards={fourthPile} />
		<Pile cards={fifthPile} />
		<Pile cards={sixthPile} />
		<Pile cards={seventhPile} />
	</section>
</main>

